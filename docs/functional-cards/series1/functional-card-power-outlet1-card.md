---
template: main.html
title: "Functional Cards: Power Outlet Card #1"
description: "Example of functional card, power outlet card #1"
hideno:
  toc
tags:
  - Design
  - Functional Card
  - Power Outlet Card
---
<!-- GT/GL -->
##:sak-sak-logo: Visualization
<div class="grid cards" markdown>

-   :sak-sak-logo:{ .lg .middle } __Outlet *"Off"*__

    ---
    ![Swiss Army Knife Functional Card Power Outlet1 D06 Light Off](../../assets/screenshots/sak-functional-card-12-power-outlet1-theme-d06-light-off.png#only-light){width="300"}
    ![Swiss Army Knife Functional Card Power Outlet1 D06 Dark Off](../../assets/screenshots/sak-functional-card-12-power-outlet1-theme-d06-dark-off.png#only-dark){width="300"}

-   :sak-sak-logo:{ .lg .middle } __Outlet *"On"*__

    ---

    ![Swiss Army Knife Functional Card Power Outlet1 D06 Light On](../../assets/screenshots/sak-functional-card-12-power-outlet1-theme-d06-light-on.png#only-light){width="300"}
    ![Swiss Army Knife Functional Card Power Outlet1 D06 Dark On](../../assets/screenshots/sak-functional-card-12-power-outlet1-theme-d06-dark-on.png#only-dark){width="300"}
</div>
This card uses the [Material 3 theme D06, TealBlue][ham3-d06-url]

| Description| Aspect Ratio| Target Size |
|-|-|-|
| A card that controls the on/off state of a power outlet, but also displays the power value. <br>Both using a segmented arc and as state.| 3/1 | Grid with 2 columns |

| SAK Tool| Used for |
|-|-|
| Circle | The half circle, as the left part of the circle is cutoff by the card. Animated, state dependent|
| Icon | Entity Icon. Animated, state dependent|
| Name | Name of Entity|
| State | Secondary Info of entity|
| Line | Vertical line separator|
| SegArc | Half segmented arc showing the sensors state with 4 colors|
| State | Entity State|
| Switch | Switch to indicate and control the state. Animated, state dependent|

##:sak-sak-logo: Interaction

| Part | Description|
|-|-|
| Switch | Toggles the power switch |
| Card | All tools connected to an entity do show by default the "more-info" dialog once clicked |

##:sak-sak-logo: Usage
[:octicons-tag-24: 1.0.0-rc.3][github-releases]

!!! warning "Replace example entities with your entities!"

```yaml linenums="1"
- type: 'custom:swiss-army-knife-card'
  entities:
    - entity: sensor.washingmachine_energy_power
      name: 'PwrOutl #1'
    - entity: sensor.washingmachine_energy_power
      secondary_info: last_changed
      format: relative
    - entity: switch.washingmachine_energy
      name: 'Air'
  layout:
    template:
      name: sak_layout_fce_power_outlet1
      variables:
        - sak_layout_power_outlet_segarc_scale_max_watt: 200
```

| Data | Default| Required | Description |
|-|-|-|-|
| entities |  | :material-check: | The single entity on the card |
| sak_layout_power_outlet_segarc_scale_max_watt | 200 | :material-check: | The max value of the scale |


##:sak-sak-logo: YAML Template Definition
[:octicons-tag-24: 1.0.0-rc.3][github-releases]
??? Info "Full definition of layout template"
    ```yaml linenums="1"
      sak_layout_fce_power_outlet1:
      template:
        type: layout
        defaults: 
          - sak_layout_power_outlet_segarc_scale_max_watt: 200
      layout:
        aspectratio: 3/1
        toolsets:
          # ================================================================
          - toolset: half-circle
            position:
              cx: 0                             # Center on cards border 
              cy: 50
            tools:
              # ------------------------------------------------------------
              - type: circle
                position:
                  cx: 50
                  cy: 50
                  radius: 48
                styles:
                  circle:
                    fill: none
                    stroke: var(--theme-sys-color-secondary)
                    stroke-width: 3em
                    opacity: 0.5

          # ================================================================
          - toolset: column-icon
            position:
              cx: 25
              cy: 50
            tools:
              # ------------------------------------------------------------
              - type: icon
                position:
                  cx: 50
                  cy: 50
                  align: center
                  icon_size: 30
                entity_index: 0
                styles:
                  icon:
                    fill: var(--theme-sys-color-secondary)
                
          # ================================================================
          - toolset: column-name
            position:
              cx: 120
              cy: 50
            tools:
              # ------------------------------------------------------------
              - type: name
                position:
                  cx: 50
                  cy: 50
                entity_index: 0
                styles:
                  name:
                    text-anchor: middle
                    font-size: 25em
                    font-weight: 700
                    opacity: 1
              # ------------------------------------------------------------
              - type: state
                position:
                  cx: 50
                  cy: 80
                entity_index: 1
                show:
                  uom: none
                styles:
                  state:
                    text-anchor: middle
                    font-size: 14em
                    font-weight: 500
                    opacity: 0.7

          # ================================================================
          - toolset: line1
            position:
              cx: 200                           # On 1/3 of card width
              cy: 50
            tools:
              # ------------------------------------------------------------
              - type: line
                position:
                  cx: 50
                  cy: 50
                  orientation: vertical
                  length: 50
                styles:
                  line:
                    fill: var(--primary-text-color)
                    opacity: 0.5

          # ================================================================
          - toolset: column-power
            position:
              cx: 250
              cy: 50
            tools:
              # ------------------------------------------------------------------------
              - type: state
                position:
                  cx: 50
                  cy: 50
                entity_index: 0
                styles:
                  state:
                    text-anchor: middle
                    font-size: 20em
                    font-weight: 700
                    fill: var(--primary-text-color)
                  uom:
                    fill: var(--primary-text-color)
                    font-weight: 700

              # ------------------------------------------------------------------------
              - type: 'segarc'
                position:
                  cx: 50
                  cy: 50
                  start_angle: -90                            # Arc clockwise from
                  end_angle: 90                               # -90 to 90 degrees
                  width: 6
                  radius: 40                                # Radius on 100x100 grid
                entity_index: 0
                scale:
                  min: 0
                  max: '[[sak_layout_power_outlet_segarc_scale_max_watt]]'
                  width: 6
                  offset: 12
                show:
                  scale: false                              # Disable scale of segarc
                  style: 'colorlist'
                segments:
                  colorlist:
                    gap: 1                                  # Gap between segments
                    colors:
                      - var(--theme-sys-palette-primary50)  # Use 4 system palette
                      - var(--theme-sys-palette-primary45)  # colors that adhere
                      - var(--theme-sys-palette-primary40)  # to light and dark
                      - var(--theme-sys-palette-primary35)  # theme modes!
                styles:
                  foreground:
                    fill: darkgrey
                  background:
                    fill: var(--theme-sys-elevation-surface-neutral4)
                    opacity: 1

          # ================================================================
          - toolset: switch
            position:
              cx: 250                           # On 1/3 of card width
              cy: 80
              scale: 3
            tools:
              # ------------------------------------------------------------
              - type: switch
                position:
                  cx: 50
                  cy: 50
                entity_index: 2
                user_actions:
                  tap_action:
                    haptic: light
                    actions:
                      - action: call-service
                        service: switch.toggle
    ```

<!-- Image references -->

<!--- Internal References... --->
[Swiss Army Knife Tutorial 02]: ../tutorials/10-step-tutorial-02-intro.md

<!--- External References... --->
[ham3-d06-url]: https://material3-themes-manual.amoebelabs.com/examples/material3-example-theme-d06-tealblue/
[github-releases]: https://github.com/amoebelabs/swiss-army-knife-card/releases/
