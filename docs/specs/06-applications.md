# 06 — Application Pages

Phase 5. Route root: `/applications/*`. Generic app experiences, each a
self-contained 2/3-pane layout using Resizable + Sidebar.

### Mail — `/applications/mail`
- Purpose: Email client shell
- Sections: Folder sidebar (Inbox, Starred, Sent, Drafts, Archive, Trash) → message list (middle pane) → reading pane (right, Resizable)
- Components: Sidebar, Resizable, List, Avatar, Badge (unread count)
- Data entities: `messages`
- States: E (empty folder), L, Er, Sel (multi-select for bulk actions)

### Chat — `/applications/chat`
- Purpose: Team chat / DM shell
- Sections: Workspace switcher → Channels + Direct messages list (left) → Conversation (center) → Message composer (bottom)
- Components: Sidebar, MessageScroller, Message, Bubble, Attachment, Marker (per shadcn chat rules in the `shadcn` skill)
- Data entities: `messages`
- States: E (no messages), L (loading history), streaming-follow

### Calendar — `/applications/calendar`
- Purpose: General-purpose calendar app (distinct from the CRM/PM calendar blocks — this is the full app shell)
- Sections: Toolbar (Month/Week/Day/Agenda) → Calendar grid → Upcoming events sidebar
- Components: Calendar, Card, List
- Data entities: `events`
- States: E, L, Er

### Notes — `/applications/notes`
- Purpose: Notes app shell
- Sections: Notes sidebar (folders/tags) → Note list → Note editor (rich text area)
- Components: Sidebar, Textarea/editor area, Command (search), Badge (tags)
- Data entities: `notes`
- States: E, L, Er, unsaved-draft indicator

### Files — `/applications/files`
- Purpose: File manager shell
- Sections: Folder tree sidebar → Files table/grid toggle → Preview panel (right, Resizable)
- Components: Sidebar, Table, Card (grid mode), Resizable, ContextMenu (file actions)
- Data entities: `files`
- States: E (empty folder), L, Er, upload-progress

### Notifications — `/applications/notifications`
- Purpose: Notification center
- Sections: Filter tabs (All/Unread/Mentions/System) → Notification timeline
- Components: Tabs, List, Avatar, Badge
- Data entities: `notifications`
- States: E, L, Er, F

## Build notes
- These are lower priority than the dashboard families — build after
  `05-dashboards-other-families.md` unless a specific block from here (e.g.
  Notifications' timeline) is needed earlier by a dashboard page.
- Mail and Chat share the same 3-pane Resizable shell — implement once as a
  layout, reuse for both.
