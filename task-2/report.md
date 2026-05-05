Prototyping with Lovable Project Report

Tools & Techniques:

Frontend: React, Tailwind CSS, Lucide Icons.

Backend/DB: Supabase (PostgreSQL, Real-time, Auth, Storage).

Platform: Lovable.ai for rapid prototyping.

Notable Decisions:

Visual Identity: Developed a "Liquid Window" style with blue/light-blue gradients and pixel-cutout corners to resonate with the motion design community.

Smart Covers: Implemented a dual-cover system where the main gallery remains clean with generative covers, but event pages can display custom photography.

RSVP Logic: Used direct Supabase RPC calls for reliable attendee counting and FIFO waitlist management.

Challenges:

CSV Export: Encountered browser-level blocking for downloads within the Lovable preview iframe. Fixed by implementing a robust Blob-based download trigger accessible via a standalone tab.

RLS Policies: Configured complex Row-Level Security to allow public visibility of Host profiles while protecting sensitive attendee data.