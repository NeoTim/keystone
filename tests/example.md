# Keystone Example Model

This file contains an example model for Keystone. For an example of the raw
modeling language, see [example.km](example.km).

```keystone
  -- Keystone model definitions can be embedded into Markdown documents by using
  -- GitHub-style code fences marked with the 'keystone' language identifier.

  -- This file contains a raw Keystone model. For an example of Keystone models
  -- embedded in Markdown, see example.md.

  -- Comments start with the "--" delimiter.

  -- Interfaces describe the externally-visible operations of a system.

  interface DatabaseApi is
  end DatabaseApi;

  interface RestApi is
  end RestApi;

  -- Components describe atomic units of the system decomposition.
  -- They can fulfill interface specifications, and depend on them.

  component ExampleComponentA is
    fulfill DatabaseApi;
    require MonitoringApi;
  end ExampleComponentA;

  component ExampleComponentB is
    fulfill RestApi;
    require DatabaseApi;
    require MonitoringApi;
  end ExampleComponentB;

  -- Systems combine components and other systems into larger units, and may also
  -- contain channels that connect the components via their interfaces.
  system SimpleSystem is
    PartA: ExampleComponentA;
    PartB: ExampleComponentB;
    connect PartA to PartB via DatabaseApi;
    -- Systems may also fulfill interfaces via their subcomponents, and declare
    -- dependencies for them.
    fulfill RestApi;
    require MonitoringApi;
  end SimpleSystem;

  system CompositeSystem is
    Frontend: SimpleSystem;
    Backend: ExampleComponentB;
  end CompositeSystem;

```
