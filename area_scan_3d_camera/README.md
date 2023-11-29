# HALCON Samples

This documentation provides descriptions of the HALCON samples for Mech-Eye Industrial 3D Camera.

For more detailed information on controlling Mech-Eye Industrial 3D Camera with HALCON, please refer to the [user manual](https://docs.mech-mind.net/en/eye-3d-camera/latest/genicam/genicam.html).

## Prerequisites for Controlling Camera with HALCON

1. [HALCON](https://www.mvtec.com/downloads) 20.11 or above has been installed on the computer.
2. [Mech-Eye SDK 2.0.0](https://downloads.mech-mind.com/?tab=tab-sdk) or above has been installed on the computer.
3. Camera firmware version is consistent with Mech-Eye SDK version. If not, use Mech-Eye Viewer or the [firmware upgrade tool](https://docs.mech-mind.net/en/eye-3d-camera/latest/api/api-camera-firmware-update.html) to upgrade the camera firmware.
4. The IP addresses of the camera and the computer Ethernet port connected to the laser profiler are in the same subnet. Use Mech-Eye Viewer or the [IP configuration tool](https://docs.mech-mind.net/en/eye-3d-camera/latest/api/api-ip-configuration.html) to set the camera IP address.

## Connect to Camera

This section describes the method for connecting to a specific camera. This method is used in all samples.

1. Open the sample in HDevelop.
2. Obtain all the available cameras by running the `info_framegrabber` operator (press the F6 key).
3. Select a camera to connect:

    (1) In the **Control Variables** area, double-click **DeviceInfos** to display a list of all the available cameras.
    (2) In the list, double-click the camera to which you want to connect, and copy the camera name after **unique_name:** or **user_name:**.

    > Note: The camera name after **user_name:** is the custom camera name set in Mech-Eye Viewer. For instructions, please refer to the [user manual](https://docs.mech-mind.net/en/eye-3d-camera/latest/viewer/connect-to-camera-and-set-ip.html#set-camera-name).

    (3) In the **Program Window**, locate the following line, and replace `MechEye` with the copied camera name.

    ```halcon
    DeviceInfo := 'MechEye'
    ```

4. Run the sample by pressing the F5 key. The selected camera will be connected.

> Note:
>
> * After executing the entire sample, please press the F2 key to reset program execution. Otherwise, the camera cannot be connected by Mech-Eye Viewer.
> * If a point cloud is displayed in the **Canvas** window, please click the orange **Continue** button in this window to continue the program execution. Otherwise, the program is stuck in the `visualize_object_model_3d` operator and will not proceed.

## Description of Samples

* [connect_to_camera_and_capture_images](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/area_scan_3d_camera/connect_to_camera_and_capture_images.hdev):  
  Connect to the camera, obtain the 2D image and point cloud, and adjust the camera parameters.
* [configure_camera_ip_address](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/area_scan_3d_camera/configure_camera_ip_address.hdev):  
  Obtain the current IP address, subnet mask, and gateway settings of the camera and modify these settings.
* [obtain_depth_map](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/area_scan_3d_camera/obtain_depth_map.hdev):  
  Obtain the depth map only, which is a 2D image that contains only the Z values of the points. Intended for reducing cycle time.
* [obtain_textured_point_cloud](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/area_scan_3d_camera/obtain_textured_point_cloud.hdev):  
  Obtain 3D data and the 2D image used for texturing the point cloud, and then construct the textured point cloud.
* [obtain_point_cloud_with_normals](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/area_scan_3d_camera/obtain_point_cloud_with_normals.hdev):  
  Obtain the point cloud with normals.
* [hand_eye_calibration](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/area_scan_3d_camera/hand_eye_calibration):
  Two samples used to perform hand-eye calibration.
