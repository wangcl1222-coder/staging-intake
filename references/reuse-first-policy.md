# Reuse-first handoff policy

Every compiled intake must carry:

```yaml
reuse_first:
  required: true
  discovery_order:
    - official_capabilities
    - installed_skills_plugins
    - user_assets_github
    - official_sdks_reference_implementations
    - high_quality_skills_open_source
    - adapted_combination
    - build_new
```

This sequence is a constraint for a future Planner. `staging-intake` records it but does not perform discovery, select a tool, or recommend an implementation. The final `build_new` option is reached only after the earlier options have been checked and found insufficient.

