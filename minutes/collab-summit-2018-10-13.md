# Node.js collaboration summit session: Open standards & Web compatibility

- **Date** 13 October 2018
- **Location** Vancouver Convention Centre West Building, 1055 Canada Place Vancouver, British Columbia V6C 0C3 Canada

## Links

- **Remote participation**: https://zoom.us/j/383984667
- **GitHub Issue**: https://github.com/nodejs/summit/issues/106

## Agenda

### 1. Organization (5min)

- Setting up Zoom
- Find note takers
- Format of this session

### 2. Goals of this session (5min)

- To review the current status of Web compatibility in Node.js
- To discuss around the **process** that we wish to implement in **Node.js core** regarding standards participation, implementation, and compatibility with the Web
- To discuss about the organization of the open standards effort
- To come up with actionable items that we can follow up on after this session

### 3. State of web compatibility in Node.js core (5min)

- APIs implemented with existing Web APIs in mind, but without conformance tests
  - Web Workers
  - Timers
  - Web Messaging
- APIs implemented with the specification in mind and/or covered with Web Platform Tests
  - url (URL, URLSearchParams)
  - console
  - encoding (TextEncoder/TextDecoder)
  - performance-timeline (perf_hooks)
- Current status of interoperability between Node.js APIs and Web APIs

### 4. Implementing existing standards in core (25min)

- The process for proposing to implement, implementing and shipping standards in core
  - What should be part in the proposal to implement
    - Matteo: does the API make sense for Node.js?  Not all APIs make sense for Node.js. They may be browser-only.
    - User should be able to identify potential for non-recoverable errors as early as possible.
    - Do we want to implement Fetch or is it fundamentally different from what Node.js should offer?
  - It is desirable to follow browser patterns as much as is practical.
  - For example, with workers: There are people that are going to want to write multithreaded code that they can share between browser and Node.js. What will build tools need to do to make Node.js workers browser-compatible? We should be thinking about that. Would be helpful to have the input/viewpoint of those who are already experimenting with these things.
  - Things that are exposed in the browser as a global, we should be clear about whether ours is exposed or needs to be required, whether ours is the same or different, etc.
  - We’re going to keep having this conversation until we are at the table more often when the spec is being written. Even something as basic as timers is difficult to implement correctly in Node.js. We need to have these conversations earlier, and not coming to them after-the-fact.

- How do we seek consensus on whether to implement a standard in core?
  - Current process: issue in core repo => proof of concept => argue in the issue tracker => lands
  - Small core vs batteries-included: we should have shared values and meta consensus to start from
  - Why small core? Do we want it small because there is a small delta with the browser or do we want it small so that there is a small surface area.
  - We are always going to navigate between the small core and batteries-included
- How to integrate upstream tests (e.g. Web Platform Tests)  into core and report about conformance
  - We should be compatible if possible.
  - We should have comparative data. Sometimes browsers don’t stay completely on spec for example. 
  - What happens if the tests do not cover implementation-defined behaviors
  - Gus: there’s already a movement to make wpt platform independent - i think we should support that as much as possible
  - We should automate all this work, rather than the current copy/paste error-prone methodology. CITGM-type thing maybe?

- How to improve documentation for interoperability between existing APIs and Web APIs
  - Documentation: Recipes on how to consume lookalike APIs in an adaptive format (so-called “isomorphic code”) that champion better practices on adapting to the different platforms (Node.js, browser, etc.).
  - Actively document the intended differences between Node.js and Web APIs.
  - A collapsible-table in the docs might be good. “Yes, we have Fetch, but here are the things we do and don’t do.”
  - Since we always have to do a partial implementation on our way to our target, there will always be a need to document what is and isn’t there.
  - Please do not come up with different names that are 80% the same. Use the same name and document the 20% that is different.
  - If it’s global, the implication is that it’s the same.

### 5. Standards that we may be interested in implementing (5min)

Brainstorming here.

- Fetch
- WHATWG Streams
- ES Modules
- WebUSB
- Web Locks
- WebCrypto: no streaming, missing essential APIs in core, propose an official npm package under @nodejs => scoped modules, needs implementation
  - Should we encourage people to use it or not?
  - It’s more about one API for both environment and there is only one option
- ServiceWorker
- WebRTC
- Scoped Modules

### 6. Participation in standards bodies for future standards (15min)

- How we can provide constructive feedback to standards bodies and represent the spectrum of opinions in core
   - How we should describe the agreement and disagreement in core
   - Surveys, how to collect the opinions in core
   - Standards bodies may not be able to take Node.js project’s opinions into account when they design specifications if they don’t know the opinion of the Node.js project. (Core devs on Node.js often disagree with each other.) 
  - Implement as experimental features. Concrete implementation before spec is finalized would help a lot.
  - Counterpoint: It’s not that simple. Spec’ing Node.js behavior for standards bodies does not always matter. We should shoot for it mattering, but it’s an uphill battle. (First step: Show up. WHATWG assumes browsers = everyone and that is not the case.)
  - Representatives for different opinions
  - Showing up at: ECMA (actual meeting in a room), WHATWG (email, usually), W3C (mix)
  - Make sure the standards bodies think of Node’s use cases
  - Pre-meetings
- What communication channel (e.g. meetings, conferences, IMs, GitHub) we can use to
    - Synchronize about our work
    - Report to other collaborators/the community about the status of our work
    - Get feedback from the community and to improve inclusivity
    - Looking at other WGs, video calls, GitHub issues
- Partnership opportunities between standards bodies
  - Specify node-related things
    - What would that mean? Node.js can be incompatible with Node.js specs?
    - JS environments that are not browsers in general
    - node-chakracore, Electron, IoT.js
  - Help standard bodies with organizational work (meetings, participation process, documentation)
    - ECMA community programs for invited experts
    - Joint foundation opportunities
  - What should image be in standards bodies? What are our values? Visions?
    - (Didn’t get to discuss about this because we ran out of time)
