---
colorSchema: light
favicon: /public/images/diracx-logo-square.png
color: orange-light
layout: cover
routerMode: hash
title: DIRAC+X status
theme: neversink 
neversink_string: "The 11th DIRAC Users' Workshop"
---

# DIRAC+X status

**Federico Stagni** <Email v="federico.stagni@cern.ch" />

September 17th 2025
__ <a href="https://indico.cern.ch/e/duw11" class="ns-c-iconlink"><mdi-open-in-new />The 11th DIRAC Users' Workshop</a>  


---
layout: section 
color: lime-light
---

<div style="display: flex; align-items: center; justify-content: center;">
    <img id="DIRAC" src="/public/images/DIRAC-logo-extended.png" alt="DIRAC logo" style="width: 300px;">
    <span style="margin: 0 50px;">--></span>
    <img id="DiracX" src="https://raw.githubusercontent.com/DIRACGrid/management/master/branding/diracx/svg/diracx-logo-full.svg" alt="DiracX" style="width: 300px;">
</div>

---
layout: side-title
color: gray-light
title: Architecture
align: cm-lm
titlewidth: is-3
---


:: title ::

# Architecture diagram

:: content ::

<img id="D_X" src="/public/images/architecture.png" class="mx-auto"> </img>


---
layout: top-title
color: gray-light
align: c
title: Versions
---

:: title ::

# Versions

:: content ::

```mermaid
%%{init: { 'logLevel': 'debug', 'theme': 'base', 'timeline': {'disableMulticolor': true}}}%%
timeline
    May 2022 : DIRAC v8.0
    Oct 2023 : EOL DIRAC v7.3
             : First DiracX demo
    Q1 2025  : DIRAC v9.0
             : DiracX v0.0.1
             : can start using DiracX services
```

<SpeechBubble position="r" color='cyan' shape="round"  v-drag="[20,211,148,240]">
Current production and only supported version, used by all DIRAC installations
</SpeechBubble>


<SpeechBubble position="l" color='amber' shape="round"  v-drag="[780,265,140,175]">
DIRAC v9 and DiracX 0.0.1 will be released together.
</SpeechBubble>

---
layout: top-title-two-cols
color: gray-light
align: c-lm-lm
title: DiracX v0.0.1
---

:: title ::

# Getting to **DiracX 0.0.1** -- [road map](https://github.com/DIRACGrid/diracx/blob/main/docs/ROADMAP.MD)

:: left ::

* First release contains:
    * All service/client underpinnings
    * Extension support
    * JobStateUpdateHandler can be replaced by DiracX

:: right ::

**To complete before declaring that is "ready"**

- [ ] Finish any DIRAC v9 cleanups
- [ ] Get LHCbDIRAC certification running stably with DIRAC v9
- [ ] Finish legacy adapter for JobStateUpdateClient
- [ ] Admin VO
- [ ] Ensure the helm chart is stable for updates
- [ ] Make sure the docs are complete

---
layout: top-title
color: gray-light
align: cm
title: Status
---

:: title ::

# Today's status

:: content ::

- 

---
layout: top-title
color: gray-light
align: cm
title: v9
---

:: title ::

# And which functionalities are in **DIRAC v9**?

:: content ::

- The concept of "Setup" is disappearing
- You will need OpenSearch (or ElasticSearch)
- Using DIRAC's RSS (Resource Status System) is mandatory
- DIRAC's ARC and ARC6 Computing Element are not supported anymore

&nbsp;
&nbsp;


Basically: no new functionalities, but many changes for DiracX. Lots of database schema changes.

---
layout: section
color: cyan-light
title: toV9
---

# From DIRAC v8 to v9+0.0.1

---
layout: top-title-two-cols
color: gray-light
align: c-lm-lm
title: Deployments
---

:: title :: 

# DiracX is deployed on Kubernetes

:: left ::

Kubernetes - <devicon-kubernetes class="text-3xl align-middle inline-block mx-0"></devicon-kubernetes> Standard to define a distributed system

<ul class="text-sm">
  <li>Separates infrastructure from applications
    <ul>
      <li class="text-xs">"Please IT department(/cloud provider) run this for me"</li>
    </ul>
  </li>
</ul>


Helm <devicon-helm class="text-3xl align-middle inline-block mx-0"></devicon-helm> gives the ability:

<ul class="text-sm">
  <li>to parameterise</li>
  <li>to distribute a kubernetes config</li>
</ul>

:: right ::

<ul class="text-sm">
  <li><a href="https://github.com/DIRACGrid/diracx-charts">DiracX Helm chart</a>
    <ul>
      <li>If your institution provides a kubernetes service: use it</li>
      <li>If you work with public clouds: use their container services</li>
      <li>Alternatively, follow these <a href="https://github.com/DIRACGrid/diracx-charts/tree/master/k3s">k3s instructions</a></li>
    </ul>
  </li>
  <li>Used for:
    <ul>
      <li>DiracX testing (GitHub actions)</li>
      <li>Local development instance</li>
      <li>Running a demo instance</li>
      <li>Running test and productions instances</li>
    </ul>
  </li>
</ul>


<StickyNote color="gray-light" textAlign="center" width="260px" title="What to run on K8" v-drag="[175,430,600,100]">
The helm charts provide "everything", inclusing MySQL and Opensearch. You are in no obligation to run all available services on K8
</StickyNote>



---
layout: top-title
color: gray-light
align: c
title: v9-migration
---

:: title ::

# What is in practice needed to migrate to v9?

:: content ::

Use this [skeleton](https://codimd.web.cern.ch/5C44tUJTReacVOcIn_0Bfg#), but first of all:

- You need an IdP (IAM...) -- you probably already have one instance!
  - Probably one for every VO you host (?)
- Register a DiracX `client` in the IdP, will be needed in order for DiracX (server) to authenticate
- if you have a VODIRAC extension:
  - update it considering the many changes.
  - code an "empty" `vodiracx` extension
- if you have a WebAppDIRAC extension:
  - code an "empty" `vodiracx-web` extension
- have a k8 project ready for hosting (vo)diracx
- deploy (vo)diracx 

---
layout: top-title
color: gray-light
align: c
title: FutureExtensions
---

:: title ::

# DiracX extensions

:: content ::

<span class="bg-cyan-100 text-cyan-600 text-center p-4 border-l-6 border-2 border-cyan-400 rounded-lg pl-8 pr-8 w-full block">
    By now, we know that it is sometimes necessary to extend all Dirac(X) components 
    
    DiracX aims to provide an easy way to do so.
</span>


```toml
# entrypoints in pyproject.toml

[project.entry-points."diracx.db.sql"]
AuthDB = "diracx.db.sql:AuthDB"
JobDB = "<extension>.db.sql:ExtendedJobDB"
```

<SpeechBubble position="t" color='amber' shape="round"  v-drag="[400,310,220,140]">
For DiracX and DiracX-Web we already provide reference extensions
</SpeechBubble>


---
layout: top-title
color: gray-light
align: c
title: Migration
---

:: title ::

### Business continuity for DIRAC communities is our top priority
Services of DIRAC v9 and DiracX will need to live together for some time


:: content ::

<Arrow x1="300" y1="170" x2="370" y2="170" />
<Line :x1=345 :y1=200 :x2=345 :y2=500 :width=1 />

<Arrow x1="610" y1="170" x2="680" y2="170" />
<Line :x1=633 :y1=200 :x2=633 :y2=500 :width=1 />

<div style="display: flex; align-items: center; justify-content: center;">
    <img id="D_X" src="/public/images/legacy_before_Adaptor.png" class="mx-auto w-1/4"> </img>
    <img id="D_Ad" src="/public/images/legaxyAdaptor.png" class="mx-auto w-1/4"> </img>
    <img id="X" src="/public/images/legacy_after_Adaptor.png" class="mx-auto w-1/4"> </img>
</div>

<SpeechBubble position="r" color='cyan' shape="round"  v-drag="[100,350,40,60]">
1
</SpeechBubble>

<SpeechBubble position="r" color='cyan' shape="round"  v-drag="[370,350,40,60]">
2
</SpeechBubble>

<SpeechBubble position="r" color='cyan' shape="round"  v-drag="[660,350,40,60]">
3
</SpeechBubble>

<SpeechBubble position="t" color='amber' shape="round"  v-drag="[160,350,120,180]">
DIRAC and DiracX share the databases
</SpeechBubble>

<SpeechBubble position="t" color='amber' shape="round"  v-drag="[430,350,160,180]">
A legacy adaptor moves traffic from DIRAC to DiracX services
</SpeechBubble>

<SpeechBubble position="t" color='amber' shape="round"  v-drag="[720,350,120,140]">
DIRAC services can be removed
</SpeechBubble>

---
layout: section
color: cyan-light
title: Demos
---

# Demonstrations


---
layout: iframe-right
title: Web API
url: https://diracx-cert.app.cern.ch/api/docs
class: webAPI
slide_info: false
color: gray-light
align: lm
---

# DiracX Web API

<AdmonitionType type='caution' >
What is on the right is the certification Web API (VOs: `dteam` and `gridpp`), loaded live. Use with caution!
</AdmonitionType>

DIRAC Web APIs with <devicon-fastapi-wordmark class="text-7xl align-middle inline-block mx-0"></devicon-fastapi-wordmark>

<ul class="text-sm">
  <li>
    Nicely documented by 
    <devicon-swagger-wordmark class="text-7xl align-middle inline-block mx-0"></devicon-swagger-wordmark>
    <ul class="text-xs ml-4">
      <li class="text-xs">--> this is what you see on the right</li>
    </ul>
  </li>
  <li>
    Follows the <devicon-plain-openapi-wordmark class="text-7xl align-middle inline-block mx-1"></devicon-plain-openapi-wordmark> specification, with the (python) client generated by <a href="https://github.com/Azure/autorest/blob/main/docs/introduction.md">AutoREST</a>.
  </li>
</ul>


<!-- 
- there is also redoc
- AutoREST supports several langagues, not only python
-->


---
layout: top-title
color: gray-light
align: c
title: CLI
---

:: title ::

# CLI Interactions

:: content ::

1. Logging in (using the `diracx cli`):

```bash
❯ dirac login gridpp
Logging in with scopes: ['vo:gridpp']
Now go to: https://diracx-cert.app.cern.ch/api/auth/device?user_code=XYZXYZXYZ
...Saved credentials to /home/fstagni/.cache/diracx/credentials.json
Login successful!
```

2. Submitting a job (using Python `requests`):

```python
import requests

requests.post('https://diracx-cert.app.cern.ch/api/jobs/', headers={'accept': 'application/json', 'Authorization': 'Bearer eyJhbG...', 'Content-Type': 'application/json'}, json=jdl)
```

3. Getting its status (using `curl`):

````md magic-move
```bash
curl -X 'GET' \
  'https://diracx-cert.app.cern.ch/api/jobs/status?job_ids=8971' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer eyJhbG...'  | jq
```
```json
{
  "8971": {
    "Status": "Done",
    "MinorStatus": "Execution Complete",
    "ApplicationStatus": "Unknown"
  }
}
```
````


---
layout: iframe-left
title: WebApp
url: https://diracx-cert.app.cern.ch
class: webapp
slide_info: false
color: gray-light
align: lm
---

# DiracX web

We are also rewriting [the Web App](https://github.com/DIRACGrid/diracx-web) from scratch.

Software stack:
- NextJS <devicon-nextjs-wordmark class="text-4xl align-middle inline-block mx-2" />
- Material UI <devicon-materialui class="text-3xl align-middle inline-block mx-2" />
- TypeScript <devicon-typescript class="text-3xl align-middle inline-block mx-2" />

<AdmonitionType type='caution' >
What is on the left is the certification WebApp, loaded live. Use with caution!
</AdmonitionType>

---
layout: top-title
color: gray-light
align: c
title: LHCb
---

:: title ::

# LHCbDIRAC and LHCbDiracX

:: content ::

# show extensions "live"

---
layout: section
color: cyan-light
title: Conclusions
---

# To conclude

---
layout: side-title
color: gray-light
title: Contribute
align: cm-lm
titlewidth: is-3
---

:: title ::

# *"I want to contribute"*

:: content ::

## The obvious ways:

<ul class="text-sm">
    <li>
        <a href="https://github.com/DIRACGrid/diracx" class="text-blue-600 hover:underline">code (github.com/DIRACGrid)</a>
    </li>
    <li>
        tests: (as you could see we have a somewhat open test deployment infrastructure). Try something out, and let us know!
    </li>
</ul>

**Run the demo (on your laptop):**

```sh
git clone https://github.com/DIRACGrid/diracx-charts
diracx-charts/run_demo.sh # this is run for each and every commit in Github Actions
```
 

## Discuss:
<ul class="text-sm">
  <li><strong>mattermost</strong>: <a href="https://mattermost.web.cern.ch/diracx/" class="text-blue-600 hover:underline">https://mattermost.web.cern.ch/diracx/</a></li>
  <li><strong>meetings</strong>: (almost) every week on Thursday morning (CET)</li>
  <li><strong>hackathons</strong>: we have been doing 2-days DiracX hackathons every quarter, at CERN
    <ul class="text-xs ml-4">
      <li>--> <a href="https://indico.cern.ch/event/1458873/" class="text-blue-600 hover:underline">Last one yesterday and the day before</a></li>
      <li>--> <a href="https://indico.cern.ch/event/1443765/" class="text-blue-600 hover:underline">Next will be in April</a></li>
    </ul>
  </li>
  <li><strong>workshops</strong>: once per year, more or less
    <ul class="text-xs ml-4">
      <li>--> <a href="https://indico.cern.ch/event/1433941/" class="text-blue-600 hover:underline">Next one in September 2025, in Beijing</a></li>
    </ul>
  </li>
</ul>



<!-- 
- You might have seen that we set up 2 VOs: **gridpp** and **dteam**. For **dteam** we do not import all members, but if you want to...
-->



---
layout: top-title-two-cols
align: cm-cm-lm
color: orange-light
columns: is-4
title: summary
--- 
:: title ::

# Summary

:: left :: 

<img id="DiracX" src="https://raw.githubusercontent.com/DIRACGrid/management/master/branding/diracx/svg/diracx-logo-square.svg" class="mx-auto w-4/5"> </img>

:: right ::

<ul class="text-base">
  <li>DiracX is "the neXt Dirac incarnation", ensuring the future of the widely used Dirac
    <ul class="text-sm">
      <li>We are rewriting the code, but it is still Dirac that you love!</li>
    </ul>
  </li>
</ul>


---
layout: credits
color: navy
loop: true
speed: 1.0
title: credits/people
---


<div class="grid text-size-4 grid-cols-3 w-3/4 gap-y-10 auto-rows-min ml-auto mr-auto">
    <div class="grid-item text-center mr-0- col-span-3">
        <strong>People</strong><br> 
    </div>
    <div class="grid-item text-right mr-4 col-span-1">
        <strong>Current Developers, maintainers, supporters</strong>
    </div>
    <div class="grid-item col-span-2">
        Chris Burr <i>CERN, LHCb</i><br/>
        Christophe Haen <i>CERN, LHCb</i><br/>
        Alexandre Boyer <i>CERN, LHCb</i><br/>
        Natthan Piggoux <i>LUPM (FR), CTA</i><br/>
        Cedric Serfon <i>Brookhaven National Laboratory (US), Belle2</i><br/>
        Ryunosuke O'Neil <i>CERN, LHCb</i><br/>
        Daniela Bauer <i>Imperial college (UK), GridPP</i><br/>
        Simon Fayer <i>Imperial college (UK), GridPP</i><br/>
        Janusz Martyniak <i>Imperial college (UK), GridPP</i><br/>
        Xiaomei Zhang <i>Beijing, Inst. High Energy Phys. (CN), Juno</i><br/>
        Luisa Arrabito <i>LUPM (FR), CTA</i><br/>
        André Sailer <i>CERN</i><br/>
        Jorge Lisa Laborda <i>Univ. of Valencia and CSIC (ES), LHCb</i><br/>
        Bertrand Rigaud <i>IN2P3 (FR)</i>
    </div>
    <div class="grid-item text-right mr-4 col-span-1">
        <strong>Project lead</strong>
    </div>
    <div class="grid-item col-span-2">
        Federico Stagni <i>CERN, LHCb</i><br/>
        Andrei Tsaregorotsev <i>CPPM (FR), EGI and LHCb</i>
    </div>
</div>

&nbsp;
&nbsp;
&nbsp;

<div class="grid-item col-span-3 text-center mt-180px mb-auto font-size-1.5rem">
    <strong>Questions?</strong>
</div>

---
layout: section
color: cyan-light
title: Backup
---

# Backup
