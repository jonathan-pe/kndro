# ADR-001: Mobile Stack and Styling/UI Architecture

## Status

Accepted

## Context

The **kndro** platform aims to provide a modern, performant, and extensible mobile application for iOS and Android, aligned with our web frontend (React + TypeScript). The mobile app must support:

- Cross-platform development with shared logic
- High-quality UI with a design system approach
- Ease of development, debugging, and future extensibility
- Seamless integration with Expo for CI/CD, OTA updates, and native device features

Existing options for styling and UI components include:

- Utility-first styling: **NativeWind** / **Uniwind**
- Component libraries: **React Native Paper**, **Tamagui**, **Gluestack UI**

Key tradeoffs:

| Option             | Pros                                                              | Cons                                                                |
| ------------------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| NativeWind         | Tailwind-like, lightweight, fast, highly extensible               | Styling-only, needs component primitives                            |
| Gluestack UI       | Prebuilt, customizable components, Expo-focused, TypeScript ready | Smaller community than RN Paper, some setup/config required         |
| Tamagui            | High performance, design token support, cross-platform            | Steep learning curve, less adoption                                 |
| React Native Paper | Stable, mature, well-documented                                   | Material Design aesthetic, less flexible for custom design language |

## Decision

We will adopt the **Gluestack UI + NativeWind** approach for mobile development.

- **NativeWind** will provide utility-first styling, mirroring our web Tailwind workflow.
- **Gluestack UI** will provide a set of prebuilt, customizable components optimized for Expo and TypeScript.
- Custom components will be built on top of Gluestack + NativeWind to implement our own **design language** and maintain consistent theming.
- This combination balances **stability, adoption, ease of use, performance, and extensibility**.

## Consequences

- **Positive**
  - Rapid UI development with prebuilt, customizable components
  - Utility-first styling ensures consistent, maintainable design
  - Compatible with Expo and React Native best practices
  - Easy to extend and integrate with custom design tokens and themes
  - Familiar workflow for web/mobile parity (Tailwind-based styling)

- **Negative / Tradeoffs**
  - Gluestack UI adoption is smaller than legacy libraries like RN Paper — minor risk of delayed community support
  - Some setup/config is required to integrate NativeWind with Gluestack UI
  - NativeWind is a styling system only; additional primitive components must be defined to complete the design system

- **Future Considerations**
  - Consider Tamagui for performance-critical screens if scaling across web + mobile
  - Review and update library versions periodically to track community adoption and support
  - Encourage component-first development to maintain a clean separation of design tokens, styling, and logic

## Mobile Stack Overview (Updated)

- **Framework & Language:** React Native (Expo), TypeScript
- **Navigation:** TanStack Router / React Navigation
- **State Management:** Zustand
- **Styling:** NativeWind (utility-first, Tailwind-inspired)
- **UI Components:** Gluestack UI + custom primitives built with NativeWind
- **Networking:** Axios
- **Device Features:** Push notifications, location services, camera/media access, offline caching
- **Performance:** React Native Reanimated for animations, code splitting/lazy loading, asset optimization
- **Testing:** Jest, React Native Testing Library, Detox for E2E
- **Deployment:** Expo OTA updates, CI/CD via GitHub Actions, TestFlight / Google Play beta channels
