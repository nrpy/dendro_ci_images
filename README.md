# NRPy Dendro Apptainer

CPU-only build environment for qualifying NRPy-generated Dendro-GR modules.
The official Ubuntu OCI image uses the `ubuntu:24.04` tag; the definition
upgrades it and refuses to build unless the resulting userspace is Ubuntu
24.04.5.

Build from this directory so `%files` can find `requirements.txt`:

```bash
cd .dendro_apptainer
apptainer build dendro-ubuntu24.04.5.sif Apptainer.def
```

The image exports read-only source templates through `DENDRO_GR_SOURCE`,
`DENDROLIB_SOURCE`, `TOML11_SOURCE`, and `SPDLOG_SOURCE`. Copy the two Dendro
trees into a writable directory before adding and building generated code.
Their shallow Git metadata is retained so a writable copy can fetch other
revisions. Upstream documentation and figures are omitted because they are not
part of generated-module builds.
Supply the cached header-only dependencies during CMake configuration:

```bash
-DFETCHCONTENT_SOURCE_DIR_TOML11="$TOML11_SOURCE" \
-DFETCHCONTENT_SOURCE_DIR_SPDLOG="$SPDLOG_SOURCE"
```
