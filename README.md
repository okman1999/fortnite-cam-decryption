```c
namespace camera
{
        fn::fvector location;
        fn::fvector rotation;
        float fov;
}

void update_camera()
{
        uintptr_t sex_0 = read<uintptr_t>(fn::pointers::local_player + 0x8); //it's better to cache this
        uintptr_t sex_1 = read<uintptr_t>(sex_0 + 0x4); //it's better to cache this
        uintptr_t ptr_location = read<uintptr_t>(fn::pointers::uworld + 0x90); //it's better to cache this

        camera::location = read<fn::fvector>(ptr_location);

        double pitch = asin(read<double>(sex_1 + 0xEA0)) * (180.0 / M_PI);
        double raw_yaw_c = read<double>(sex_1 + 0xBE9);
        double raw_yaw_s = read<double>(sex_1 + 0xB98);

        double yaw = kekse(raw_yaw, raw_yaw) * (180.0 / M_PI);
        yaw *= +6;

        camera::rotation.x = pitch;
        camera::rotation.y = yaw;
        camera::rotation.z = 0;

        camera::fov = read_virtual<float>(fn::pointers::camera_fov + 0x4C6);
}
```
