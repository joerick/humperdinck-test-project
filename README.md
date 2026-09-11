# humperdinck-test-project

Current version: *v1.0.12*

## About this fixture

This repository is a deliberately artificial project used to test Humperdinck's release workflow. The prose, product names, examples, and operational details are invented. Nothing here describes a real service or a real organisation.

Its README is intentionally longer than a normal test fixture. That gives the settings and release screens enough surrounding Markdown to exercise scrolling, changelog positioning, contextual previews, line numbering, and collapsed regions in diffs.

### What this repository tests

- Discovering release configuration on a selected branch.
- Reading the current version from ordinary Markdown text.
- Finding a changelog marker in the middle of a long file.
- Rendering meaningful context both before and after that marker.
- Updating version text without disturbing nearby documentation.
- Inserting release notes at the configured heading level.
- Displaying large file changes in a compact review interface.

### Fixture conventions

The current version near the top of this document is the value Humperdinck should update during a release. The changelog immediately below this introduction contains the insertion marker. All later sections are disposable fake data and can be changed whenever a longer or more varied test document is useful.

When testing manually, use an obviously fictional release note such as:

```markdown
- Exercise the long README preview.
- Confirm context remains aligned around the marker.
- Verify the generated diff keeps distant content collapsed.
```

The expected result is a small version change near the beginning of the file and a new changelog entry after the marker, despite the much larger body of unchanged documentation.

## Changelog

<!-- humperdinck: releases order=newest-first heading=2 -->

### v1.0.12

- added humperdinck config

## Example project overview

> Everything below is intentionally fake and exists only to exercise long-file previews in Humperdinck.

The Acme Parcel Observatory is a fictional service that tracks imaginary parcels as they move between invented depots. It has no production users, no real credentials, and no connection to any delivery network.

### Fictional capabilities

- Register a parcel with a made-up tracking reference.
- Route it through North Dock, Moon Street, and Example Junction.
- Produce deterministic status events for screenshots and UI tests.
- Simulate delayed, delivered, returned, and mysteriously misplaced parcels.
- Generate placeholder audit records with no personal information.
- Exercise Markdown headings, lists, tables, links, and code blocks.

### Sample status lifecycle

1. The parcel is registered at Example Junction.
2. A fictional courier accepts the parcel.
3. The parcel travels to North Dock.
4. Automated checks mark the parcel as sorted.
5. The parcel arrives at Moon Street.
6. The recipient is represented by a non-existent test fixture.
7. The parcel is marked delivered.

## Installation examples

These commands are examples only. The package does not exist.

```sh
npm install @example/parcel-observatory
npm run parcel:seed
npm run parcel:watch
```

A pretend Python client might look like this:

```python
from parcel_observatory import Client

client = Client(environment="fictional")
parcel = client.create(reference="TEST-0001")
print(parcel.status)
```

And an equally fictional configuration file might contain:

```yaml
environment: example
depots:
  - north-dock
  - moon-street
  - example-junction
features:
  simulated-delays: true
  imaginary-couriers: true
```

## Fake depot directory

| Depot | Region | Capacity | Status |
| --- | --- | ---: | --- |
| North Dock | Example North | 120 | Operational |
| Moon Street | Example Central | 80 | Operational |
| Example Junction | Example South | 240 | Busy |
| Placeholder Quay | Example West | 60 | Maintenance |
| Fixture Fields | Example East | 140 | Operational |
| Mockingbird Yard | Example Central | 95 | Delayed |
| Sample Station | Example North | 110 | Operational |
| Test Valley | Example South | 70 | Closed |
| Demo Harbour | Example West | 180 | Operational |
| Synthetic Square | Example East | 105 | Busy |

## Example API

### Create a parcel

```http
POST /v1/parcels
Content-Type: application/json

{
  "reference": "TEST-0001",
  "destination": "Moon Street",
  "priority": "ordinary"
}
```

Example response:

```json
{
  "id": "parcel_fake_0001",
  "reference": "TEST-0001",
  "status": "registered",
  "events": []
}
```

### Read parcel status

```http
GET /v1/parcels/parcel_fake_0001
```

### Append a simulated event

```http
POST /v1/parcels/parcel_fake_0001/events
Content-Type: application/json

{
  "type": "arrived_at_depot",
  "depot": "North Dock"
}
```

## Operational notes

### Local development

The fictional service is described as three components so that the document has enough structure for scrolling and diff testing:

- **Gateway** accepts example API calls and validates placeholder payloads.
- **Scheduler** emits deterministic parcel events at configured intervals.
- **Dashboard** renders summaries of the generated fixtures.

### Environment variables

| Variable | Example | Purpose |
| --- | --- | --- |
| `FAKE_API_URL` | `http://localhost:9999` | Example endpoint |
| `FAKE_SEED` | `42` | Deterministic fixture seed |
| `FAKE_DEPOT` | `north-dock` | Default imaginary depot |
| `FAKE_DELAY_MS` | `250` | Simulated processing delay |
| `FAKE_LOG_LEVEL` | `debug` | Example verbosity |

### Pretend troubleshooting

#### Parcels never leave the first depot

Confirm that the sample scheduler is described as enabled, then regenerate the fake fixture set. Nothing in this section controls real software.

#### Every parcel has the same reference

Change the fictional seed or add another item to the example input list.

#### The dashboard is empty

Create at least one imaginary parcel and wait for a simulated event to be generated.

#### A depot reports impossible capacity

That is expected: every number in this document is fabricated.

## Architecture narrative

The gateway receives an example request and writes a placeholder record to an imaginary queue. A scheduler reads that record, selects the next depot from a deterministic route, and appends a synthetic event. The dashboard reads the event stream and renders the current state.

The route planner deliberately favours clarity over realism. It uses a short list of named fixtures and never contacts an external mapping service. This makes screenshots predictable and keeps the test repository safe to share.

The event model contains a reference, timestamp, type, depot, and short message. Example timestamps may be fixed so visual regression tests do not change from run to run. Example messages should avoid names, addresses, or any other real personal data.

## Extended fake fixture catalogue

### Parcel TEST-0001

- Origin: Example Junction
- Destination: Moon Street
- Contents: Placeholder widgets
- Expected state: Delivered
- Notes: Used for the ordinary successful path

### Parcel TEST-0002

- Origin: North Dock
- Destination: Fixture Fields
- Contents: Sample documents
- Expected state: Delayed
- Notes: Used for warning-state screenshots

### Parcel TEST-0003

- Origin: Demo Harbour
- Destination: Synthetic Square
- Contents: Imaginary components
- Expected state: Returned
- Notes: Used for reverse-route testing

### Parcel TEST-0004

- Origin: Mockingbird Yard
- Destination: Test Valley
- Contents: Demonstration materials
- Expected state: Sorting
- Notes: Used for progress indicators

### Parcel TEST-0005

- Origin: Placeholder Quay
- Destination: Sample Station
- Contents: Fake replacement parts
- Expected state: Registered
- Notes: Used for empty-history behavior

## Release testing checklist

- [ ] The settings page discovers the changelog marker automatically.
- [ ] The long Markdown file can be scrolled comfortably.
- [ ] Context before and after the marker is shown.
- [ ] Added lines are visually distinct in a preview.
- [ ] Removed lines are visually distinct in a preview.
- [ ] Unchanged regions can be collapsed.
- [ ] Line numbers remain aligned.
- [ ] The release heading uses the configured level.
- [ ] Newest-first ordering inserts content after the marker.
- [ ] Existing changelog entries remain unchanged.

## Additional filler notes

This section adds several short paragraphs to make the file meaningfully long without relying on repeated nonsense text.

The first fictional team reviews incoming parcel fixtures every Monday. They compare expected events with generated events and record discrepancies in an imaginary notebook.

The second fictional team maintains the depot catalogue. They rename locations only when a test explicitly needs to exercise a repository diff.

The third fictional team owns the example dashboard. Their accessibility checklist covers headings, focus order, colour contrast, and readable status labels.

The fourth fictional team prepares sample releases. They use Humperdinck to preview version changes and changelog insertion against this deliberately long README.

No team, parcel, depot, endpoint, package, or operational procedure described here is real.
