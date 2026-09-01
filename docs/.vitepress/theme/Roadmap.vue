<script setup>
const principles = [
  {
    title: 'Scope before dates',
    description: 'The release moves when its required contracts are ready. Optional features do not hold alpha.'
  },
  {
    title: 'Integration over demos',
    description: 'A resource is ready when it works through supported contracts and survives restart and upgrade paths.'
  },
  {
    title: 'Documentation is release work',
    description: 'Setup, configuration, API references, ownership boundaries, and migration notes ship with the code.'
  }
]

const stages = [
  {
    date: 'Sep–Oct 2026',
    status: 'Foundation freeze',
    title: 'Stabilize the framework contracts',
    objectives: [
      'Freeze the Alpha contract surface for Core, Character, Inventory, Roles, Routing, World, and Toolkit.',
      'Finish ACL and policy ownership between Core, Admin, Inventory, and future access resources.',
      'Remove duplicate legacy surfaces from the primary documentation path.',
      'Define supported dependency and resource start order.'
    ]
  },
  {
    date: 'Nov–Dec 2026',
    status: 'Alpha candidate',
    title: 'Prove installation and integration',
    objectives: [
      'Exercise clean installs through the official recipe on Windows and Linux.',
      'Complete contract, persistence, restart, migration, and failure-path smoke tests.',
      'Validate the server-owner configuration path without requiring code changes.',
      'Publish complete API signatures, examples, and resource ownership guidance.'
    ]
  },
  {
    date: 'January 2027',
    status: 'Closed alpha',
    title: 'Run real servers on the candidate',
    objectives: [
      'Onboard a small group of server owners and resource developers.',
      'Collect installation, operations, upgrade, performance, and integration failures.',
      'Accept bug fixes and documentation corrections; defer new optional features.'
    ]
  },
  {
    date: 'February 2027',
    status: 'Stabilization',
    title: 'Resolve release blockers',
    objectives: [
      'Close critical data-loss, security, identity, permission, and lifecycle defects.',
      'Confirm recovery procedures and safe migration behavior.',
      'Lock the Alpha release notes and known limitations.'
    ]
  },
  {
    date: 'March 2027',
    status: 'Public alpha',
    title: 'Release a usable Alpha',
    target: true,
    objectives: [
      'Publish tagged, compatible resource releases and the matching recipe.',
      'Publish server-owner setup, developer references, upgrade notes, and known limitations.',
      'Open a defined support and issue-triage process for Alpha adopters.'
    ]
  },
  {
    date: 'Q2 2027+',
    status: 'After alpha',
    title: 'Measure the path to Beta',
    future: true,
    description: 'Beta timing will be based on Alpha adoption and defect trends. Future-release work such as nested containers, trading, selectable ledger themes, sorting, favorites, and optional hotbar cooldown hooks remains outside the Alpha gate.'
  }
]

const releaseGate = [
  'Clean installation succeeds from documented steps.',
  'Core gameplay resources start and report healthy contracts.',
  'Character identity and Inventory state persist safely.',
  'Permissions fail closed and administrative actions are audited.',
  'Restart and upgrade paths do not silently destroy player data.',
  'Server owners can configure the supported experience without editing source code.'
]
</script>

<template>
  <div class="feather-roadmap">
    <header class="feather-roadmap__hero">
      <div class="feather-eyebrow">Release plan</div>
      <h1>A usable alpha in Q1 2027.</h1>
      <p>Feather will call itself alpha when a server owner can install it, configure it, operate it, and upgrade it with a documented path—not simply when the individual resources run.</p>
      <div class="feather-roadmap__target">
        <span>Target window</span>
        <strong>March 2027</strong>
        <small>Public usable alpha</small>
      </div>
    </header>

    <section class="feather-roadmap__principles">
      <div v-for="principle in principles" :key="principle.title">
        <strong>{{ principle.title }}</strong>
        <p>{{ principle.description }}</p>
      </div>
    </section>

    <div class="feather-release-track">
      <article
        v-for="stage in stages"
        :key="stage.date"
        class="feather-release-stage"
        :class="{
          'feather-release-stage--target': stage.target,
          'feather-release-stage--future': stage.future
        }"
      >
        <div class="feather-release-stage__date">{{ stage.date }}</div>
        <div class="feather-release-stage__body">
          <span class="feather-release-stage__status">{{ stage.status }}</span>
          <h2>{{ stage.title }}</h2>
          <ul v-if="stage.objectives">
            <li v-for="objective in stage.objectives" :key="objective">{{ objective }}</li>
          </ul>
          <p v-else>{{ stage.description }}</p>
        </div>
      </article>
    </div>

    <section class="feather-release-gate">
      <div>
        <div class="feather-eyebrow">Alpha release gate</div>
        <h2>What “usable” means</h2>
      </div>
      <ul>
        <li v-for="requirement in releaseGate" :key="requirement">{{ requirement }}</li>
      </ul>
    </section>
  </div>
</template>
