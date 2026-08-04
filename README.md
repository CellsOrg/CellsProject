<table align="center"><tr><td>

```
   _--_     _--_    _--_     _--_     _--_     _--_     _--_     _--_
  (    )~~~(    )  (    )~~~(    )   (    )~~~(    )   (    )~~~(    )
   \           /    \           /     \           /     \           /
    (  ' _ `  )      (  ' _ `  )       (  ' _ `  )       (  ' _ `  )
     \       /        \       /         \       /         \       /
   .__( `-' )          ( `-' )           ( `-' )        .__( `-' )  ___
  / !  `---' \      _--'`---_          .--`---'\       /   /`---'`-'   \
 /  \         !    /         \___     /        _>\    /   /          ._/   __
!   /\        )   /   /       !  \   /  /-___-'   ) /'   /.-----\___/     /  )
!   !_\       ). (   <        !__/ /'  (        _/  \___//          `----'   !
 \    \       ! \ \   \      /\    \___/`------' )       \            ______/
  \___/   )  /__/  \--/   \ /  \  ._    \      `<         `--_____----'
    \    /   !       `.    )-   \/  ) ___>-_     \   /-\    \    /
    /   !   /         !   !  `.    / /      `-_   `-/  /    !   !
   !   /__ /___       /  /__   \__/ (  \---__/ `-_    /     /  /__
   (______)____)     (______)        \__)         `-_/     (______)

   
                                                      
```

</td></tr></table>

<p align="center">
  <img src="https://img.shields.io/badge/Salesforce-00A1E0?logo=salesforce&logoColor=white" />
  <img src="https://img.shields.io/badge/LWC-0176D3?logo=salesforce&logoColor=white" />
  <img src="https://img.shields.io/badge/Apex-1798C1?logo=salesforce&logoColor=white" />
  <img src="https://img.shields.io/badge/HTML-E34F26?logo=html5&logoColor=white" />
  <img src="https://img.shields.io/badge/CSS-1572B6?logo=css3&logoColor=white" />
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black" />
</p>

# Project Tongss

Project Tongss is a Salesforce CRM project inspired by the T0$$ user experience.

It connects a modern customer-facing web application with Salesforce, allowing customer interactions to flow seamlessly into CRM. The project demonstrates how a frontend application and Salesforce can work together through a clean architecture focused on usability, maintainability, and scalability.

---

## Key Features

- 🏦 T0$$-inspired customer experience
- ☁️ Salesforce CRM integration
- 👤 Customer & Account management
- 📦 Product and Order management
- 📋 Case & Service workflows
- ⚡ Apex business logic
- 🧩 Lightning Web Components (LWC)
- 🎨 Shared Design System
- 🔗 Frontend ↔ Salesforce integration

---

##  Architecture

```mermaid
flowchart TD
    A[👤 Customer]

    B["🌐 Tongss Web App<br/>HTML · CSS · JavaScript"]

    C["☁️ Salesforce Org<br/>LWC · Apex · Flow"]

    D[(Customer)]
    E[(Orders)]
    F[(Products)]
    G[(Cases)]
    H[(Reports)]
    I[(CRM Data)]

    A --> B
    B --> C

    C --> D
    C --> E
    C --> F
    C --> G
    C --> H
    C --> I
```

---

## Contributor


