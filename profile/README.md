[![SmoothSail header](https://github.com/smooth-sail/.github/blob/main/images/smoothsail-header.png)](https://smooth-sail.github.io)

> SmoothSail is a feature flag management tool with user targeting capabilities.

---

## Welcome to SmoothSail! ⛵

SmoothSail is a self-hosted, open-source feature flag tool designed for small companies aiming for rapid feature development with minimized risks. It empowers developers to separate the release of new features from their deployment and quickly revert unsuccessful updates with just a click. SmoothSail provides accurate user targeting capabilities, enabling engineers to introduce new features to specific demographics and limit the impact of unforeseen bugs in production.

📄 To learn more about SmoothSail and the decisions that went into its design, check out our [case study](https://smooth-sail.github.io/case-study)

## Getting Started

There are two ways developers can get started with SmoothSail:

- 🐳 [Docker](https://github.com/smooth-sail/smoothsail#1-setting-up-smoothsail): The easiest, and quickest, way to get up and running with SmoothSail is to to use Docker. This will run each piece of SmoothSail's architecture with limited configuration.
- 🖥️ Run locally: For developers who want complete control and customization they can run each component locally. Each SmoothSail component's GitHub repo is available with documentation to get up and running.
  - [Manager Platform](https://github.com/smooth-sail/smoothsail-manager)
  - [SDK Service](https://github.com/smooth-sail/smoothsail-sdk-service)

## Core Concepts

SmoothSail has four closely related entities at its core: Flags, Segments, Attributes, and Rules. Together they enable SmoothSail users to target segments of users within their application. To start using SmoothSail, users need to first create these entities in the SmoothSail dashboard.

- Attributes are what describe a user and can be three data types: string, numbers, or booleans. These are made up of name and a data type.
  - used to make rules and are reusable
  - Attribute examples:
    - Email string
    - Age number
    - Beta tester boolean
- Rules are a combination of attribute, operator, and value that get evaluated to place a user in a segment
  - operator examples: =, >, <, <=, >=, contains, does not contain, is, is not, exists, does not exist
  - Rule examples:
    - Email contains @gmail.com
    - Age > 18
    - Beta tester is true
- Segments are reusable collections of rules
  - Segments have a rules operator, `ANY` or `ALL`, which determine if **ANY** of the rules must be true or if **ALL** of the rules must be true to be part of that segment
- Flags are the primary entity of SmoothSail and are meant to represent a specific feature to be toggled on or off.
  - Flags are toggled off by default when created
  - Flags are made up of 0 or more segments

### User Context

User context is an object composed of attribute-value pairs that provide information about a user. This information is used with rules to evaluate if a user belongs in a segment.

## Architecture

SmoothSail's architecture consists of four major parts:

- The **Manager Platform** manages flag data. It is also responsible for performing authentication and managing SDK keys.
- The **SDK Service** establishes and maintains Server-Sent Events (SSE) connections with authenticated SDKs.
- **NATS JetStream** facilitates reliable communication between the Manager and SDK Service.
- The **SDK**s are embedded into the developer's application and are responsible for connecting to the SDK Service. SDKs are also responsible for evaluating flag data for any user context the developer decides to pass in.

[![SmoothSail architecture](https://github.com/smooth-sail/.github/blob/main/images/smoothsail-architecture.png)](https://smooth-sail.github.io/case-study)

## The Team

**[Emily Olszewski]()** _Software Engineer_ • Tucson, AZ

**[Bradley Taylor]()** _Software Engineer_ • Las Vegas, NV

**[Dariia Vyshenska]()** _Software Engineer_ • Seattle, WA

**[Isaac Lee]()** _Software Engineer_ • Los Angeles, CA
