# Monopod Suction Bucket Foundation – Rodrigues Rotation

## Overview
Numerical simulation of multidirectional loading on a **monopod suction bucket** foundation for offshore wind turbines, using **Rodrigues rotation** for 3D tilt representation.

This is an upgraded version of the [original monopod demo](https://github.com/sinahdme/monopod_suction-bucket-demo), which used Euler angles. The Rodrigues axis-angle formulation eliminates gimbal lock and preserves directional symmetry for all tilt directions, consistent with the [tripod](https://github.com/sinahdme/tripod-suction-bucket) and [tetrapod](https://github.com/sinahdme/tetrapod-suction-bucket) repositories.

## Key improvement: Rodrigues vs Euler

| Aspect | Original (Euler) | This version (Rodrigues) |
|--------|------------------|--------------------------|
| Rotation method | Sequential rotations about fixed axes (phi, theta, psi) | Single axis-angle rotation via Rodrigues formula |
| Parameters | 3 Euler angles | Tilt magnitude `dd` + direction `alpha_deg` |
| Gimbal lock | Possible at certain angles | None |
| Directional symmetry | Not preserved for all tilt directions | Preserved for all alpha values |

## File descriptions

- **MAINCODE.m** – Main solver with iterative center-of-rotation search.
- **rodrigues_rotation.m** – Builds the rotation matrix from tilt magnitude and direction using the Rodrigues formula.
- **transformation.m** – Transforms point positions from body frame to fixed frame (supports both Euler and rotation matrix input).
- **xtransformation.m** – Extended transformation for fixed-frame coordinate computation.
- **points.m** – Defines spring node locations along the bucket skirt, skirt tip, and lid.
- **coeffinder.m** – Evaluates p-y spring forces at each node.
- **coeffinder_deadload.m** – Computes p-y forces affecting t-z forces during settlement (before rotation).
- **pycurve.m** / **pycurve_tz.m** – p-y curve theory (calls `BETA13.m` and `BETA24.m`).
- **tzcurve.m** / **tzcurve_deadlaod.m** – t-z spring forces on the skirt (outer and inner walls).
- **qzcurve2.m** – q-z spring forces at the skirt tip.
- **qzcurve4.m** – q-z spring forces beneath the lid.
- **apdefiner.m** – Coefficient alpha for lateral soil resistance effect on interface normal stress.
- **fi_finder.m** – Peak friction angle as a function of soil density ratio.
- **Rankine.m** – Rankine earth pressure coefficient.
- **BETA13.m** / **BETA24.m** – Shape coefficients for p-y curves.
- **Zvalues.m** – Depth of each spring embedded in the soil.

## Usage
1. Clone this repository or download the `.zip`.
2. Open MATLAB and run `MAINCODE.m`.
3. Load-displacement (H-theta / M-theta) curves and 3D force distributions will be generated.

## Related repositories
- [monopod_suction-bucket-demo](https://github.com/sinahdme/monopod_suction-bucket-demo) – Original monopod with Euler angles
- [tripod-suction-bucket](https://github.com/sinahdme/tripod-suction-bucket) – Tripod (3-bucket) configuration
- [tetrapod-suction-bucket](https://github.com/sinahdme/tetrapod-suction-bucket) – Tetrapod (4-bucket) configuration

## License
This project is licensed under the [GPL-3.0 License](LICENSE).

## Author
**Sina Hadadi**
Ph.D. Candidate – Wind Energy (Offshore Foundations)
Kunsan National University, South Korea
Email: sinahdme@gmail.com
GitHub: [github.com/sinahdme](https://github.com/sinahdme)
