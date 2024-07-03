---
created: 2024-07-03T18:47:07.067Z
updated: 2024-07-03T18:47:07.067Z
---
https://designsystem.digital.gov/
https://github.com/uswds/uswds
https://www.npmjs.com/package/uswds

The US government has a design system called the US Web Design System, which is used in different variations across many government websites.

Two I've worked with are:

- [VA design system](https://design.va.gov/)
- [CMS design system](https://design.cms.gov/)

The USWDS was started after the excellent UK digital service released the [[gov.uk design system]]

It's kind of a pain to get started with, so I made a couple of templates to show how to get started with it, and include automated accessibility checking:

- [USWDS HTML starter](https://github.com/adhocteam/uswds_html_starter)
	- a template for a static HTML-based site using USWDS, which uses [[File watching|turbowatch]] to rebuild the site when you make changes to the HTML or CSS
- [USWDS NextJS starter](https://github.com/adhocteam/uswds_nextjs_starter)
	- a template for a [[react.js]]-based website using USWDS and [[NextJS]]

JB Hutch made a nice site to [document how you can get started](https://uswds-tailwind-docs.vercel.app/) with the USWDS and [[tailwind]]