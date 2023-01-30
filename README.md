# EzMesh

<p align="center">the open source parametric CFD mesh generator</p>

<p align="center">
    <a href="https://discord.gg/H7qRauGkQ6">
        <img src="https://img.shields.io/discord/913193916885524552?logo=discord"
            alt="chat on Discord">
    </a>
    <a href="https://www.patreon.com/turbodesigner">
        <img src="https://img.shields.io/badge/dynamic/json?color=%23e85b46&label=Patreon&query=data.attributes.patron_count&suffix=%20patrons&url=https%3A%2F%2Fwww.patreon.com%2Fapi%2Fcampaigns%2F9860430"
            alt="donate to Patreon">
    </a>
</p>



# About
EzMesh is a declarative tool that parametrically generates meshes compliant with a variety of mesh formats with easy and configurable API on top of GMSH.


# Install
```
pip install git+https://github.com/Turbodesigner/ezmesh.git#egg=ezmesh
```

# Example
See more examples in [examples](/examples) directory
## Inviscid Wedge
```python
from ezmesh.mesh import Mesh, CurveLoop, PlaneSurface
import numpy as np

with Mesh() as mesh:
    wedge_coords = np.array([[0, 1], [1.5, 1], [1.5, 0.2], [0.5, 0], [0, 0]])
    wedge_curve_loop = CurveLoop(
        wedge_coords, 
        mesh_size=0.05,
        labels={
            "upper":  [0],
            "lower":  [2,3],
            "inlet":  [4],
            "outlet": [1],
        },
        transfinite_cell_counts={
            150: [0],
            200: [1,4],
            100: [2],
            50:  [3]
        }
    )
    surface = PlaneSurface(wedge_curve_loop, is_quad_mesh=True, transfinite_corners=[0,1,2,4])
    mesh.generate(surface)
    mesh.write("mesh_wedge_inv.su2")
```

![Inviscid Wedge](./assets/inviscid_wedge_mesh.png)


# Devlopement Setup
```
git clone https://github.com/Turbodesigner/ezmesh.git
cd ezmesh
pip install -r requirements_dev.txt
```

# Help Wanted
Right now there are some items such as more CFD meshing configurations. Please join the [Discord](https://discord.gg/H7qRauGkQ6) for project communications and collaboration. Please consider donating to the [Patreon](https://www.patreon.com/turbodesigner) to support future work on this project.
