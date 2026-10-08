# FluentQt

**A Fluent Design UI framework for Python desktop applications (PyQt5), in two editions: Community and Pro.**

FluentQt is an independent software project: a component library and application foundation for building modern,
fast, accessible desktop tools in Python. Community covers everything an ordinary application needs; Pro adds advanced
components for professional tools, including computer-vision and monitoring UIs. Both are used every day by the
applications listed at the end of this page.

![Portfolio](https://img.shields.io/badge/portfolio-showcase_only-1F3A5F)
![Source](https://img.shields.io/badge/source-private-6B6B6B)
![Qt](https://img.shields.io/badge/Qt-PyQt5_5.15-41CD52)
![Python](https://img.shields.io/badge/python-3.9%2B-3776AB)

> **About this repository.** It presents FluentQt through screenshots and a written overview. It contains no source
> code: the source of both editions is private at this stage.

![An operations dashboard built with FluentQt Community, light theme](assets/community/app-dashboard-light.png)

| At a glance | |
|---|---|
| **What** | A PyQt5 component framework: controls, application shells, frameless windows, theming, icons, data views, persistence. |
| **Community** | 177 widgets and layouts in 12 families, 309 icons, light/dark/system themes with any accent, high contrast, reduced motion, text scaling, six translations, frameless windows with native snap and Mica on Windows 11, SQLite persistence. |
| **Pro** | Data grid, property inspector, filter bar, a chart system, dashboard layouts, computer-vision overlays (detections, segmentation, heat maps, tracks, zones, poses), camera walls and video timelines, inspection verdicts, node-graph and region editors, code editors, command palette, task queues, wizards and guided tours. |
| **Dependency direction** | Community ← Pro ← applications. Pro uses only Community's public API; Community depends on nothing but PyQt5 and darkdetect. Enforced by tests. |

---

## Community

| | |
|---|---|
| ![Notes app, dark theme](assets/community/app-notes-dark.png) | ![Music app: carousel, album grid and now-playing bar](assets/community/app-music-light.png) |
| A notes application in the dark theme | A media application: carousel, grid and a now-playing bar |
| ![Settings app: setting cards bound to a config](assets/community/app-settings-dark.png) | ![The component gallery](assets/community/gallery-home-light.png) |
| Setting cards bound to a typed configuration | The gallery: every component beside the code that builds it |

![The splash screen while loading](assets/community/splash-light.png)

A splash screen that runs the application's loading steps, shows progress and handles failures.

## Pro

![The Pro gallery: navigation with every component page, and an object detection workspace](assets/pro/gallery-light.png)

| | |
|---|---|
| ![Incident desk: data grid, filter bar, property inspector](assets/pro/app-incident_desk-light.png) | ![Store analytics: stacked bars, donut, gauges](assets/pro/app-analytics-dark.png) |
| Data grid, filter bar and property inspector | Charts, gauges and a dashboard layout |
| ![Weekly activity heatmap and a correlation matrix](assets/pro/gallery-dashboard-charts-light.png) | ![Responsive dashboard grid with an accordion side panel](assets/pro/gallery-layouts-dark.png) |
| Heatmaps and matrices | Responsive dashboard grid |

### Computer vision and monitoring

The scenes in these screenshots are drawn procedurally by the gallery; no camera footage or third-party images are used.

| | |
|---|---|
| ![Detection workspace with confidence and IoU sliders and a synchronised list](assets/pro/vision-detection-light.png) | ![Semantic segmentation with view modes and class areas](assets/pro/vision-segmentation-light.png) |
| Detections, thresholds, class legend and live FPS/latency, all bound to one overlay | Segmentation: original, mask, overlay and side-by-side views |
| ![A GOOD/NG inspection station with defect counts and thresholds](assets/pro/vision-inspection-light.png) | ![A CCTV wall with detections, trails, a counting line and a zone alert](assets/pro/video-cctv-light.png) |
| A GOOD/NG inspection station: verdict, thresholds, counters, history | A multi-camera wall with tracking, counting lines and zone alerts |
| ![Tracking and counting with trails and in/out totals](assets/pro/video-tracking-light.png) | ![A sign-in form on frosted glass over an animated background](assets/pro/effects-glass.png) |
| Tracks, trails and counting | Visual effects: frosted glass over live content |

---

## Engineering

**Component contract.** Every component in both editions follows the same rules: colours are read from the palette at
paint time (a theme change is a repaint, never a stylesheet rebuild or a walk over the widget tree); one theme
subscription per widget; painted composites instead of nested child widgets; popups created once and reused; keyboard
access with one tab stop per composite control; sizes on a 4 px grid.

**Performance is a release requirement.** A benchmark suite measures startup, construction, theme switches, icons,
animation and frame timing, and a comparison step fails a build when a metric regresses by more than 25 %. Selected
measurements (medians, WSL2, Python 3.12, Qt 5.15):

| Measurement | Result |
|---|---|
| `import fluentqt` (families load lazily on first use) | 2.7 ms |
| Theme switch with 1,000 live widgets, until painted | 140 ms |
| Line chart: repaint 100,000 points | 2.1 ms |
| 309 icons, cold read and render | 21.6 ms |
| Leaked theme connections after 500 create/destroy cycles | 0 |

**Built to ship.** Patterns that survive Nuitka compilation, applications packaged as standalone folders with Nuitka, a persistence layer with numbered migrations and one transaction per logical operation, and long work kept
off the GUI thread (worker processes for inference and heavy compute).

**Clean-room.** FluentQt is written independently. Other Fluent-style libraries were studied for behaviour only, and a
provenance check guards against copied code. Icons are Microsoft's Fluent UI System Icons (MIT).

---

## Built with FluentQt

| | | |
|---|---|---|
| ![ChessForge](assets/apps/chessforge.png) | ![ComicTranslator](assets/apps/comic-translator.jpg) | ![Audio Story](assets/apps/audio-story.png) |
| [**ChessForge**](https://github.com/pntrungbk15/chessforge-showcase): a local chess workstation with Stockfish analysis, training and neural-network training. | [**ComicTranslator**](https://github.com/pntrungbk15/comic-translator-showcase): translate manga, manhwa and comics locally with real models (detection, multilingual OCR, LLM translation, inpainting) and project-wide proofreading. | [**Audio Story**](https://github.com/pntrungbk15/audio-story-showcase): an AI studio for narrated audio stories with LLM writing help and local TTS. |

| | |
|---|---|
| ![ScanDoc AI](assets/apps/scandoc-ai.png) | ![WebIntel Logistics](assets/apps/webintel-logistics.png) |
| [**ScanDoc AI**](https://github.com/pntrungbk15/scandoc-ai): Document AI for scanned logistics documents — enhancement, OCR, field extraction, validation and boxes on the scan; 88.9 % field accuracy on a held-out synthetic benchmark. | [**WebIntel Logistics**](https://github.com/pntrungbk15/webintel-logistics): web intelligence for logistics — crawling, structured extraction, normalization, validation and change events; 97.5 % field accuracy on a held-out synthetic benchmark. |

The industrial portfolio applications are built with FluentQt as well, for example
[SNY — Septa Line Inspection](https://github.com/pntrungbk15/sny-septa-line-inspection) and
[MFG/EXP Reading](https://github.com/pntrungbk15/mfg-exp-reading).

## Author

Phạm Ngọc Trung · [github.com/pntrungbk15](https://github.com/pntrungbk15)

All screenshots © Phạm Ngọc Trung. Shown here for portfolio purposes; no licence to the software is granted by this
repository.
