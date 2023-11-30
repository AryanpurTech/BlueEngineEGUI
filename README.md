# Blue Engine egui plugin

This is a plugin that adds [egui](egui.rs/) support to the [Blue Engine](https://github.com/AryanpurTech/BlueEngine).

## Getting started

To get started, initialize the plugin:

```rust
let gui_context = blue_engine_egui::EGUI::new(&engine.event_loop, &mut engine.renderer);
```

This will essentially initializes the egui and create things required to run the plugin. The engine will then run it twice, once before everything else to fetch all inputs and events, and then during render, so that it displays the GUI. And all that's left, is to add the plugin to the engine and use it:

```rust
engine.plugins.push(Box::new(gui_context));
```

During the update_loop, you can get the plugin back and use it. We'll assume only one plugin is added:

```rust
// -- update loop start
    // change the plugin_index from 0 to the index of the plugin when added
    let egui_plugin = let egui_plugin = plugins[0]
                // downcast it to obtain the plugin
                .downcast_mut::<blue_engine_egui::EGUI>()
                .expect("Plugin not found");
// -- rest of update loop code
```

Finally you can use it to add GUI code:

```rust
// -- rest of update loop code

// start the GUI addition
egui_plugin.ui(
    // get the context
    |ctx| {
        // create the window
        gui::Window::new("title").show(ctx, |ui| {
            // add components
            ui.horizontal(|ui| {
                ui.label("Hello World!");
            });
        });
    },
    &window,
);

// -- rest of update loop code
```

Congrats now you have a working GUI!

## Style Block

*The guide will come soon, it's cool I promise!*

## Examples

Check the [examples](https://github.com/AryanpurTech/BlueEngineEGUI/tree/master/examples) folder for potential UIs and as template for your new projects.

## Dependency justification

* `blue_engine`: Used obiously for exporting some components and struct declrations required to design the API
* `egui-wgpu`: Used to assist in applying egui to wgpu graphics backend. Which is same graphics backend used in Blue Engine.
* `egui-winit`: Support for Winit windowing. Which is same windowing system used in Blue Engine.
* `egui`: The egui itself, required to obtain components and declrations for api design.
