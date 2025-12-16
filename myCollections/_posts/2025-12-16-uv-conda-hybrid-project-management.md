---
layout: post
title:  Hybrid Project Management with uv and Conda
author: Bruce Liu
#last update date
date:   2025-12-16 15:00:00 +0800
#first published date
published: 2025-12-16 15:00:00 +0800
categories: [post]
tags: [python, conda, uv]
description: 
header-image: 
permalink: /uv-conda-hybrid-project-management/
---

Managing scientific projects often requires balancing system-level dependencies (GDAL, PROJ, HDF5) with Python package reproducibility. Conda and uv serve complementary roles.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

Managing scientific projects often requires balancing system-level dependencies ([GDAL], [PROJ], [HDF5]) with Python package reproducibility. [Conda] and [uv] serve complementary roles:

- [Conda] excels at installing compiled libraries and cross-language dependencies.

- [uv] provides fast, modern dependency resolution and reproducible lockfiles for Python packages.

## Why Hybrid?

- Geospatial and climate libraries (e.g., [GDAL], [rasterio]) are best installed via [Conda-forge].

- Python-only packages ([numpy], [pandas], [scikit-learn]) are faster and more reproducible with [uv].

- Combining both ensures stability and speed.

## Workflow Template

- Create [Conda] Environment

```sh
conda create -n hydro-env python=3.11 gdal proj 
```

or

```sh
conda env create -f environment.yml
```

Activate the new environment:


```sh
conda activate hydro-env
```

- Install [uv] Inside [Conda]

```sh
pip install uv
```

or

```sh
conda install conda-forge::uv
```

simply, installing `uv` with the virtual environment creating.

```sh
conda create -n hydro-env -c conda-forge python=3.11 gdal proj uv
```

- Initialize [uv] Project

Navigating into the project directory, and initializing it:

```sh
uv init
uv add numpy pandas rasterio
```

This creates `pyproject.toml` and `uv.lock` inside the project, aligned with [Conda]’s Python. Or synchronizing the environment when setting up on a new machine with `uv.lock`

```sh
uv sync
```

- Run Scripts

```sh
uv run script.py
```

This ensures dependencies from `uv.lock` are resolved while [Conda] provides system libraries.

- [Jupyter] Integration

```sh
uv add jupyter
```

then:

`uv run jupyter notebook` or `uv run jupyter lab`

## Best Practices

- Keep `environment.yml` for [Conda] (system deps).

- Keep `pyproject.toml` + `uv.lock` for [uv] (Python deps).

- Document both so collaborators can choose [Conda] or [uv] depending on their workflow.

- Align `.python-version` with [Conda]’s Python to avoid mismatches.

## Conclusion

The hybrid approach leverages [Conda]’s strength in compiled libraries and [uv]’s speed in Python dependency management. For geo-related projects, this ensures reproducibility, portability, and efficiency across diverse research teams.

## Related commands

- Export the [Conda] environment to a YAML file using this command:

`conda env export > environment.yml`

- Check the available [Jupyter] kernels: 

`uv run jupyter kernelspec list`

- Remove a virtual environment managed by [uv], simply delete the directory `.venv`.

- Remove a Conda environment:

```sh
conda deactivate
conda env remove --name hydro-env
```

## References

[Working on projects - uv Astral Docs](https://docs.astral.sh/uv/guides/projects/)

<!--links-->
[uv]: https://github.com/astral-sh/uv
[Conda]: https://github.com/conda/conda
[GDAL]: https://github.com/OSGeo/gdal
[PROJ]: https://github.com/OSGeo/PROJ
[HDF5]: https://github.com/HDFGroup/hdf5
[rasterio]: https://github.com/rasterio/rasterio
[Conda-forge]: https://conda-forge.org/
[numpy]: https://github.com/numpy/numpy
[pandas]: https://github.com/pandas-dev/pandas
[scikit-learn]: https://github.com/scikit-learn/scikit-learn
[Jupyter]: https://jupyter.org/
