# PyRoll Rolling Simulation Framework

Welcome to The PyRoll Project!

PyRoll is an OpenSource rolling framework, aimed to provide a fast and extensible base for rolling simulation.
The current focus lies on groove rolling in elongation grooves.
The core package includes the basic data structures and algorithms.
Further functionality is provided via [extension packages](https://pyroll.readthedocs.io/en/latest/extensions/index.html) and model approaches are provided via [plugin packages](https://pyroll.readthedocs.io/en/latest/plugins/index.html).

## Documentation

See the [documentation](https://pyroll.readthedocs.io/en/latest) to learn about basic concepts and
usage.

## License

The project is licensed under the [BSD 3-Clause license](LICENSE).

## Contributing

Feel free to open issues, or, fork and open pull requests, if you want to contribute to the core.
If you want to implement model approaches for use with PyRolL, create your own plugin package using our [plugin template](https://github.com/pyroll-project/pyroll-plugin-template).
To learn how to write plugins and extensions, please read the [documentation](https://pyroll.readthedocs.io/en/latest) and refer to the numerous existing plugins and extensions available at the [organization's GitHub page](https://github.com/pyroll-project).

### Policy for Inclusion of Hooks in the Core

Since version 2.0 we try to include as many hooks as possible into the core, to tie down the nomenclature.
This seems necessary, since for the same concepts, often different terms exist in literature.
To avoid collisions and redundancies, it is better to include these hooks in the core, although some of them may come without implementation.
This improves the exchangeability of plugins.
If you like a hook to be included in the core, open an issue, or preferably, a pull request with the respective changes.
Supply your pull request with fallback implementations of the hook, if any meaningful exist.

From this policy we explicitly exclude hooks, that are solely of use for one model approach, namely "coefficients".
They are large in number across the whole plugin landscape, but usually named after the model and of no further use to other plugins.
So the benefit from including them in the core is small, while the pollution of the core would be exzessive.
If another plugin has to make use of them, just add a dependency for the respective source plugin.

A few examples for clarification:

- The hooks `Profile.surface_temperature` and `Profile.core_temperature` may be of interests to many plugins.
  The core provides fallbacks which just return `self.temperature`, which is a good first estimate of those.
  So plugins modelling surface and thermal effects can easily refer to the respective temperatures, without worrying, if there is a model describing the temperature gradient or not.
- The hook `Profile.freiberg_flow_stress_coefficients` from the `pyroll-freiberg-flow-stress` plugin makes no sense without the Freiberg flow stress model, so it is not included in the core.
- The hook `Profile.thermal_conductivity` is a material property useful to many plugins, but no meaningful fallback exists, since there is no default material.
  So the provision of values or implementations is deferred to the user or developers of material databases.

So the core includes several hooks, that are not used by other core functionality, but provide a save ground for plugins.