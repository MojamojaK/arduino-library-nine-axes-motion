9 Axes Motion Library
-----------
The NineAxesMotion.cpp and NineAxesMotion.h files are C++ wrapper codes for the
BNO055.c and BNO055.h Sensor API. The wrapper code has been designed to
abstract the Sensor API and also to give an idea on how to use the
advanced features in the Sensor API. Apart from that it acts a bridge
between the Sensor API and the Arduino framework. Copy this library into
"yourArduinoInstallation"/libraries folder.

(追記) Euler_SaveCalにキャリブレーションに必要なオフセット値の読取り、書き込みの例を記載しております。

67, 158行目
```
mySensor.setOperationMode(OPERATION_MODE_CONFIG);
```
で読取り&書き込み可能モードしている。このモードの間は設定しか行えないため、測定はできない。

71行目
```
mySensor.setOperationMode(OPERATION_MODE_NDOF);
```
で9軸モード(NDOF = Nine Degrees Of Freedom)にしている。このモードの間は測定とキャリブレーションが行われる。

159~161行目
```
mySensor.readAccelOffset(accel_offset);
mySensor.readMagOffset(mag_offset);
mySensor.readGyroOffset(gyro_offset);
```
で各センサのオフセット値を各メソッドのパラメータに入れた配列に代入する。
これらの値を保存して電源を入れた際に書き込みを行えばキャリブレーションを行わずに起動ができる。


-------------------------------------------------------------------------------
There are 4 examples with the 9 Axes Motion library.

 - BareMinimum: This example code is as the name says the minimum code
	required to use the 9 Axes Motion shield.

 - Euler: This example code reads out the Euler angles in the NDoF mode to
	the Serial Monitor. It also reads out the Calibration Status. Each sensor
	and the System itself has its own Calibration Status. See below on how to
	calibrate each of the sensors.

 - Accelerometer: This example code reads out the Accelerometer data and
	associated data which are the Linear Acceleration data, which is the
	Accelerometer data without the gravity vector, the other is the Gravity
	Acceleration data, which is only the gravity vector.

 - Motion: This example code is a game to test how steadily you can move an
	object, in this case it is the shield with the Arduino board. The goal is
	to demonstrate on how to use the Any motion and No motion Interrupts.

Calibration helps the Sensor identify its environment and automatically
determine offsets. Follow the instructions below to calibrate your sensor.

 - Gyroscope: Keep it steady and do not move it. Preferably keep it on a fixed
	surface such as a table.

 - Accelerometer: Rotate the shield slowly and pause at every 45deg for a
	second. Rotate one 1 axis at a time. Preferably rotate along 2 axes.

 - Magnetometer: Move the magnetometer in a large 8 like pattern a few times
	gently.
