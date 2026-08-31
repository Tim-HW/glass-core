# glass-core

Sensor-agnostic estimation engine shared by [glass-lio](https://github.com/Tim-HW/glass-lio)
and glass-vio: SE(3) Gauss-Newton on a manifold, IMU preintegration, marginalization, the
nav state + IMU factor, and SO(3) Jacobians. Pure CMake, no ROS — the one sensor-facing
class (`ImuInit`) speaks a plain `ImuSample` struct, not `sensor_msgs`, so callers convert
at their own boundary.

Almost entirely header-only; only preintegration and IMU init carry a `.cpp`. Vendors
[Sophus](include/sophus/) for the Lie group types (own license, see
[`include/sophus/LICENSE`](include/sophus/LICENSE)).

Consumed as a git submodule by its front ends, or built standalone:

```bash
cmake -S . -B build && cmake --build build && ctest --test-dir build
```

For the reasoning behind the solver and the estimation stages built on top of it, see
glass-lio's [doc/gauss-newton.md](https://github.com/Tim-HW/glass-lio/blob/main/doc/gauss-newton.md)
and [doc/7-tight-coupling.md](https://github.com/Tim-HW/glass-lio/blob/main/doc/7-tight-coupling.md) —
this repo holds the engine; the write-ups live with the LIO front end that motivated them.

## License

MIT — see [LICENSE](LICENSE).
