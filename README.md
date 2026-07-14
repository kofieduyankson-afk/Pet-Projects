# Pet-Projects
Here is your repository for testing out dummy projects for imporving you programming skills
Projects should  be ordganised into folders in base then have their repoistory baranches
First project is Crumpet
I actually think this is a very strong portfolio project because the underlying problem isn't "detective board"—it's **graph-based relationship management**. The detective theme is just the visualization.

That means you can market it as several different products depending on the audience:

* **Project Intelligence Platform** (for recruiters)
* **Case Management & Investigation Tool** (enterprise/security)
* **Story Planning & World Building Tool** (writers)
* **Learning Relationship Mapper** (students)
* **Knowledge Graph Visualizer** (technical audience)

The detective board is simply one visualization mode.

---

# Core Idea

Think of the application as a relational graph database built on SQL.

Every object is a **Node**.

Every connection is an **Edge**.

The detective board simply renders those nodes and edges.

Instead of storing "everything inside everything", every object connects through relationships.

```
Person
   │
   │
Relationship
   │
   ▼
Group

Person
   │
Relationship
   │
Drama

Drama
   │
Relationship
   │
Event

Event
   │
Relationship
   │
Person
```

Essentially you're building your own mini Neo4j using PostgreSQL.

---

# Major Entities

I'd actually separate them like this.

## Project / Story / Case

```
Project
--------

id
title
description
type

status

startDate
endDate

createdBy
createdAt
updatedAt
```

This is the root.

Everything belongs to one Project.

---

## Person

```
Person

id

projectId

firstName
lastName
displayName

description

avatar

notes

createdAt
```

A person can appear in multiple projects.

If you want global people you simply remove projectId and instead make a junction table later.

---

## Group

```
Group

id

projectId

name

type

description

color

icon
```

Examples

```
Police

Management

Marketing

Company

Gang

School

Family
```

---

## Event

Instead of putting timeline inside Project I'd separate it.

```
Event

id

projectId

title

description

eventDate

location

importance
```

Now timeline becomes automatic.

---

# Involvement

This is actually the most important table.

I would rename it

```
Participation
```

or

```
Assignment
```

because it works everywhere.

```
Participation

id

projectId

personId

role

status

summary

joinedAt

leftAt
```

Examples

```
Witness

Manager

Victim

Developer

Teacher

Client
```

A person can have many participations inside one project.

---

# Relationship

This is the magic.

Instead of dozens of foreign keys...

Create one generic relationship table.

```
Relationship

id

projectId

sourceType

sourceId

targetType

targetId

relationshipType

description

strength

createdAt
```

Example

```
Person
    |
Friend
    |
Person

Person
    |
Works For
    |
Company

Company
    |
Owns
    |
Building

Person
    |
Witnessed
    |
Event

Person
    |
Suspects
    |
Person
```

This becomes your graph.

---

Instead of

```
personId

groupId

eventId
```

everything becomes

```
sourceType

sourceId

targetType

targetId
```

Exactly how graph databases work.

---

# Relationship Types

Separate them.

```
RelationshipType

id

name

color

icon

direction

description
```

Examples

```
Friend

Sibling

Enemy

Reports To

Owns

Member Of

Works With

Suspects

Witnessed

Mentors

Created

Assigned

Depends On
```

Now relationships are customizable.

---

# Notes

Every node should allow notes.

```
Note

id

projectId

entityType

entityId

content

createdBy

createdAt
```

---

# Attachments

```
Attachment

id

entityType

entityId

fileName

fileType

url
```

Could hold

Images

Videos

PDFs

Voice Notes

Evidence

---

# Tags

```
Tag

id

name

color
```

Then

```
EntityTag

entityType

entityId

tagId
```

---

# Detective Board

The board itself shouldn't store data.

It stores layout.

```
Board

id

projectId

name

```

Then

```
BoardNode

id

boardId

entityType

entityId

x

y

width

height
```

Now when users drag cards...

Only x/y changes.

---

Connections don't need to exist on the board.

They already exist in Relationship.

The board simply draws them.

---

# Node Types

Every node could be

```
Person

Group

Event

Evidence

Location

Document

Task

Custom Object
```

The board doesn't care.

Everything has

```
entityType

entityId
```

---

# Detective Canvas

Imagine

```
          [Company]

             │ Works For

             │

John ───── Friend ───── Sarah

 │

Witness

 │

Robbery

 │

Occurred At

 │

Bank
```

All generated from Relationship.

---

# Nice Features

### Timeline

Automatically generated from Events.

---

### Relationship Explorer

Click John.

Highlight

Friends

Groups

Events

Companies

Tasks

Everything.

---

### Filters

Only show

* Witnesses

* Companies

* Suspects

* Developers

* Departments

---

### Heat Map

Relationship count determines node size.

Highly connected people become larger.

---

### AI Summary

Generate

> John is connected to five events, works for ACME, has reported to Sarah since 2024, and appears in three ongoing investigations.

---

### Auto Layout

Instead of manually arranging nodes

Use

Force Directed Graph

or

Dagre

to automatically organize them.

---

# Suggested Database Structure

```
Project

Person

Group

Event

Participation

Relationship

RelationshipType

Board

BoardNode

Note

Attachment

Tag

EntityTag

ActivityLog

Comment
```

---

# Tech Stack

Since you've been working with Next.js and Prisma, I'd lean into that ecosystem:

* **Frontend:** Next.js + React + TypeScript
* **Database:** PostgreSQL
* **ORM:** Prisma
* **Authentication:** NextAuth/Auth.js or your existing auth solution
* **Canvas:** React Flow (excellent for draggable node-based UIs) or a combination of React Konva and D3.js for more custom control
* **Styling:** Tailwind CSS
* **Real-time collaboration (optional):** WebSockets or Liveblocks
* **File storage:** Cloudinary, S3, or local storage during development

## Architecture

I would structure the project around layers rather than pages:

```
src/
├── app/
├── components/
│   ├── board/
│   ├── timeline/
│   ├── graph/
│   ├── person/
│   ├── project/
│   └── relationships/
├── lib/
│   ├── graph/
│   ├── prisma/
│   └── services/
├── prisma/
│   └── schema.prisma
└── types/
```

## Why this stands out

From a recruiter's perspective, this project demonstrates much more than CRUD. It showcases:

* Designing a normalized relational database with polymorphic relationships.
* Building a graph-based data model on top of SQL.
* Creating an interactive canvas with drag-and-drop and persisted layouts.
* Implementing many-to-many relationships and complex querying.
* Separating data (relationships) from presentation (board layout), a key architectural principle.

The detective aesthetic is memorable, but the underlying architecture is what makes it an impressive engineering project. By describing it as a **Knowledge Graph and Relationship Mapping Platform with an interactive visual canvas**, you'll highlight the technical depth while still having a visually engaging demo.
