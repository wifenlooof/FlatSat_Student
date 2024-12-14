import time
import board
import busio
from picamera2 import Picamera2
from adafruitlsm6ds.lsm6ds33 import LSM6DS33
from adafruit_lis3mdl import LIS3MDL

i2c = busio.I2C(board.SCL, board.SDA)

imu = LSM6DS33(i2c)

camera = Picamera2()
camera.configure(camera.create_still_configuration())

ACCELERATION_THRESHOLD = 15.0  # m/s^2

def take_picture():
    timestamp = time.strftime("%Y%m%d-%H%M%S")
    file_name = f"picture{timestamp}.jpg"
    camera.start_and_capture_file(file_name)
    print(f"Picture taken and saved as {file_name}")

print("Monitoring IMU for threshold events...")
while True:
    acceleration = imu.acceleration  # Returns (x, y, z) in m/s^2
    total_acceleration = sum([a2 for a in acceleration])  0.5  # Calculate magnitude

    print(f"Acceleration: {acceleration}, Total: {total_acceleration:.2f} m/s^2")
    if total_acceleration > ACCELERATION_THRESHOLD:
        print("Threshold exceeded! Taking a picture...")
        take_picture()
        time.sleep(2)  # Delay to avoid multiple triggers

    time.sleep(0.1)  # Polling delay
