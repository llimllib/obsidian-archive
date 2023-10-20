https://pex.readthedocs.io/

> PEX files are self-contained executable Python virtual environments. More specifically, they are carefully constructed zip files with a `#!/usr/bin/env python` and special `__main__.py` that allows you to interact with the PEX runtime. For more information about zip applications, see [PEP 441](https://peps.python.org/pep-0441/).

via [this article](https://dagster.io/blog/fast-deploys-with-pex-and-docker), where the author uses them to bundle and deploy python applications into docker images for distribution