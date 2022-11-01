# ft-fsd-path-planning

FaSTTUBe Formula Student Driverless Path Planning Algorithm

This repository contains the path planning algorithm developed by FaSTTUBe for the 2021/22 Formula Student season.

List of contributors:

- Panagiotis Karagiannis
- Albert Thelemann

The intention of this repository is to provide teams entering the driverless category with a path planning algorithm, so that they can get up and running as fast as possible. Teams are encouraged to use this repository as a basis and adapt it to their own pipeline, as well as make changes that will improve the algorithms performance.

Parts that are specific to the FaSTTUBe pipeline have been removed. The algorithm is now a standalone library that can be used in any pipeline. It is a Python package that can be installed using pip.

The algorithm requires the following inputs:

- The car's current position and orientation in the slam map
- The position of the colored cones in the slam map

The algorithm outputs:

- Samples of a parameterized b-spline with the x,y and curvature of the samples

No color inference is performed, if there are cones for which the position is known, but the color is not, they are ignored.

The codebase is written entirely in Python and makes heavy use of NumPy, SciPy, and Numba.

## Installation

The package can be installed using pip:

```bash
pip install git+ssh://git@github.com/papalotis/fsd-path-planning.git@c1e7667fc53848df2a1aa7279549033e62471c58#egg=fsd_path_planning
```

## Basic usage

```python
from fsd_path_planning import PathPlanner, MissionTypes

path_planner = PathPlanner(MissionTypes.trackdrive)
global_cones, car_position, car_direction = load_data() # you have to load/get the data, this is just an example
path = path_planner.calculate_path_in_global_frame(global_cones, car_position, car_direction)

# path is a Nx4 numpy array, where N is the number of points in the path
# the columns represent the spline parameter (distance along path), x, y and path curvature

```

![An animation demoing the path planning algorithm](animation.gif)
