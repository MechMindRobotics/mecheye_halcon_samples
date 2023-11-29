# hand_eye_calibration Samples

With these samples, you can perform hand-eye calibration and obtain the extrinsic parameters.

> Note:
>
> * Currently, the samples only support hand-eye calibration of 6-axis robots.
> * For UHP series, to perform the hand-eye calibration, the **Capture Mode** parameter must be set to **Camera1**.

## Prerequisites for Performing Hand-Eye Calibration

Before performing the hand-eye calibration, the following prerequisites must be met.

* The accuracy of the robot is good enough.
* The calibration board that came with the camera is correctly placed/attached.

  * For EIH mode: the calibration board should be placed inside the camera FOV.
  * For ETH mode: the calibration board should be attached to the robot flange.

* The 2D image is not overexposed or underexposed (circles on the calibration board are clearly visible).
* No parts of the calibration board are missing from the depth map.
* The camera intrinsic parameters are accurate (you can check the camera intrinsic parameters with Mech-Eye Viewer).

## Workflow of Hand-Eye Calibration Using the Samples

Two samples are provided for completing the hand-eye calibration:

* **determine_calibration_poses**: used to determine the calibration poses used during the hand-eye calibration.

  > Note: During hand-eye calibration, the camera needs to obtain images of the calibration board at a series of robot poses. These robot poses are the calibration poses.

* **perform_hand_eye_calibration**: used to perform the hand-eye calibration.

The general workflow of hand-eye calibration using the two samples is described below.

### Determine Calibration Poses

1. Run the **determine_calibration_poses** sample.
2. Move the robot to a candidate pose.
3. Obtain the original 2D image and check if requirements are met.
4. Obtain the 2D image with feature detection results and check if requirements are met.
5. Enter the calibration pose to the **robot_pose** JSON file.
6. Repeat until at least 15 calibration poses are determined. 

### Perform Hand-Eye Calibration

1. Run the **perform_hand_eye_calibration** sample.
2. Move the robot to the first calibration pose.
3. Perform image capturing.
4. Repeat until robot has moved to all calibration poses.
5. Calculate extrinsic parameters.

## Edit the Samples

The following information must be identical in the two samples.

* The camera to be connected
* Calibration board model

Besides, the Euler angle convention in the **robot_pose** JSON file should be set before determining the calibration poses.

### Select the Camera

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

### Set Calibration Board Model

1. Open the sample in HDevelop.
2. Set the calibration board model: The default model is BDB-5. If you are using another model, locate the following operator, and change `BDB-5` to the [calibration board model in use](#boardtype)

   ```halcon
   set_framegrabber_param (AcqHandle, 'BoardType', 'BDB-5')
   ```

### Set Euler Angle Convention and Unit

The calibration poses determined using the **determine_calibration_poses** sample need to be entered into the **robot_pose** JSON file. The default Euler angle convention in this file is `sxyz`, and the default Euler angle unit is degree. Please follow these steps to set the Euler angle convention and unit.

1. Open the **robot_pose** JSON file.
2. Set the Euler angle convention: locate the following line, and replace `sxyz` with the Euler angle convention of the robot in use. For the Euler angle conventions already supported in the sample, please refer to [Supported Euler Angle Conventions](#supported-euler-angle-conventions).

   ```halcon
   "EulerType":"sxyz"
   ```

3. Set the Euler angle unit: if you need to enter Euler angles in radiants, locate the following line, and replace `true` with `false`.

   ```halcon
   "FromDegree":true
   ```

4. Save the **robot_pose** JSON file.

## Determine Calibration Poses

Before performing the hand-eye calibration, you need to determine at least 15 calibration poses. Please follow these steps to determine the calibration poses.

1. Run the sample by pressing the F5 key. When the program runs to the line `read_char (WindowHandle, Char, ReCode)`, the program will pause and wait for command input in the following steps.

   > Note: If the camera cannot be connected, please check if it is already connected by Mech-Eye Viewer or another GenICam client.

2. Move the robot to a candidate calibration pose with the teach pendant.

   > Note: For requirements on the calibration poses, you can refer to the **Calibration** chapter in **Help** > **HALCON Reference**.

3. Press the P key to obtain the 2D image from the camera.

   * If the calibration board is not entirely captured, please move the robot and obtain the 2D image again.
   * If the entire calibration board is captured, proceed to the next step.

4. Press the T key to obtain the 2D image containing the feature detection results.

   * If the camera did not detect the circles on the calibration board, no image will be displayed in HDevelop. In this case, please move the robot and obtain the original 2D image and the 2D image containing the feature detection results again.
   * If the camera can detect the circles on the calibration board, a 2D image containing the feature detection results will be displayed in HDevelop. Please proceed to the next step.

5. Check the robot teach pendant, and enter the current robot pose to the **robot_pose** JSON file.

    > Note: It is recommended to save the pose on the teach pendant. When performing the hand-eye calibration, you can use the saved poses to move the robot.

6. Repeat steps 2 to 5 to determine more calibration poses.

7. After determining at least 15 calibration poses, press the Q key to exit the program.
8. Set the number of calibration poses in the **robot_pose** JSON file: Open the **robot_pose** JSON file, and locate the following line. Replace `15` with the actual number of calibration poses determined.

   ```halcon
   "pose_count":15
   ```

## Perform Hand-Eye Calibration

After determining the robot calibration poses, you can perform the hand-eye calibration by running the **perform_hand_eye_calibration** sample.

### Set Camera Mounting Method

Before performing the hand-eye calibration, please set the camera mounting method in the sample.

The default mounting method is Eye in Hand. If your camera is mounted in the Eye to Hand mode, please locate the following operator, and replace `EyeInHand` with `EyeToHand`.

```halcon
set_framegrabber_param (AcqHandle, 'CalibrationType', 'EyeInHand')
```

### Switch Reference Frame

The sample contains an operator that can switch the reference frame in which the point cloud is output from the camera.

The default setting is not to switch the reference frame. If you would like to switch to the robot reference frame, please locate the following operator in the **captureTranformedPointCloud** procedure, and replace `false` with `true`.

```halcon
set_framegrabber_param (AcqHandle, 'Scan3dCoordinateTransformEnable',false)
```

### Instructions

Please follow these steps to perform the hand-eye calibration.

1. Run the sample by pressing the F5 key. The sample will stop when it runs to the `stop` operator.
2. Move the robot to the calibration pose in the **robot_pose** JSON file.

   > Note: Please move the robot to the calibration poses in the exact order as they are written in the JSON file. Otherwise, the subsequent calculation of the extrinsic parameters will fail.

3. Run the sample by pressing the F5 key. The camera will perform image capturing.

4. In the **Control Variables** area, check the value of **CollectResult**.

   * If **SUCCESS** is displayed, please proceed to the next step.
   * If an error is displayed, please troubleshoot according to the [displayed error code](#extrinerrcode), and then determine the calibration poses again.

5. A message saying "Move the robot to the next calibration pose" will be displayed on the image. Please repeat steps 2 to 3.

   > Note: After the robot has moved to all the calibration poses in the **robot_pose** JSON file, when you run the sample again, the extrinsic parameters will be calculated.
  
6. In the **Control Variables** area, check the value of **CalibResult**.

   * If **SUCCESS** is displayed, then the hand-eye calibration has succeeded. In the folder where the sample is stored, you can find the **ExtrinsicParameters** TXT file that contains the extrinsic parameters and the a point cloud file whose coordinates have been transformed.
   * If an error is displayed, please troubleshoot according to the [displayed error code](#extrinerrcode), and then determine the calibration poses again.

## Supported Euler Angle Conventions

The conversion from the following Euler angle conventions to quaternions is already supported in the sample.

| Angle input order | Euler angle convention | Robot brand               |
| :----             | :----                  | :----                     |
| Z-Y'-Z''          | rzyz                   | Kawasaki                  |
| Z-Y'-X''          | rzyx                   | ABB, KUKA                 |
| X-Y-Z             | sxyz                   | FANUC, YASKAWA, ROKAE, UR |
| X-Y'-Z''          | rxyz                   | /                         |
| Z-X'-Z''          | rzxz                   | /                         |

> Note:
>
>* Even using the same Euler angle convention, different robot brands might display the Euler angles in different orders. Please input the Euler angles in the order specified in the above table.
>* If the Euler angle convention used by your robot is not listed in the above table, you need to add the conversion from this Euler angle convention to quaternions. Please refer to the code of the ·euler_to_quad· procedure in the **perform_hand_eye_calibration** sample and add your own conversion.

## Calibration Parameters

This section introduces the parameters used during hand-eye calibration.

### BoardType

This parameter is used to set the model of the calibration board in use.

Value list and descriptions:

| Value     | Description                                                                    |
| :----     | :----                                                                          |
| BDB-5     | The recommended distance from the calibration board to the camera is < 0.6 m   |
| BDB-6     | The recommended distance from the calibration board to the camera is 0.6–1.5 m |
| BDB-7     | The recommended distance from the calibration board to the camera is > 1.5 m   |
| OCB-005   | Only used for Eye-to-Hand projects with high accuracy requirements             |
| OCB-010   | Only used for Eye-to-Hand projects with high accuracy requirements             |
| OCB-015   | Only used for Eye-to-Hand projects with high accuracy requirements             |
| OCB-020   | Only used for Eye-to-Hand projects with high accuracy requirements             |
| CGB-020   | The recommended distance from the calibration board to the camera is < 0.6 m   |
| CGB-035   | The recommended distance from the calibration board to the camera is 0.6–1.5 m |
| CGB-050   | The recommended distance from the calibration board to the camera is > 1.5 m   |

### ExtrinErrCode

This read-only parameter is used to check the status codes returned during the hand-eye calibration process.

| Status code        | Description                                                                                |
| :----              | :----                                                                                      |
| SUCCESS            | Successfully executed.                                                                     |
| POSE_INVALID       | The pose format is incorrect. Please input quaternions.                                    |
| IMAGE2D_EMPTY      | The 2D image is invalid.                                                                   |
| FIND_CORNERS_FAIL  |Feature detection of the 2D image failed. Please adjust the parameters for the 2D image.    |
| DEPTH_EMPTY        | The depth map is invalid.                                                                  |
| CORNERS_3D_INVALID | Feature detection of the depth map failed. Please adjust the parameters for the depth map. |
| POSES_INSUFFICIENT | Not enough poses are input. Please input at least 15 calibration poses.                    |
