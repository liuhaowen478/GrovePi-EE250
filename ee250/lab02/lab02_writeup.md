# Reflection questions

## 4.1
Complete the sequence of linux shell commands below in your necessary to complete this scenario. Suppose you just cloned a repository that included one python file, my_first_file.py, and you now want to add a second file to your repository named my_second_file.py and push it to Github.com. (Note: create the file using the `touch` command)

```shell
git clone git@github.com:my-name/my-imaginary-repo.git
# complete the sequence
touch my_second_file.py
git add my_second_file.py
git commit -m "Added my_second_file.py"
git push
```

## 4.2
Describe the workflow you adopted for this lab (i.e. did you develop on your VM and push/pull to get code to your RPi, did you edit files directly on your RPi, etc.).  Are there ways you might be more efficient in the next lab (i.e. learning a text-based editor so you can edit natively on the RPi, understanding Git commands better, etc.)?

I developed large bulk of code on my VM and push it to GitHub. Then I pulled from GitHub on RPi. If tweaks are needed, say I missed a space when outputting to LCD, I'll fix it on RPi.

I do think this is the most efficient way of doing labs for me. I use NeoVim even on the VM but a local terminal emulator and a more powerful machine meant far more customizability and aid, such as COC + MPLS. Those tools enable faster and more accurate coding.

## 4.3
In the starter code, we added a 200 ms sleep. Suppose you needed to poll the ultrasonic ranger as fast as possible, so you removed the sleep function. Now, your code has just the function ultrasonicRead() inside a while loop. However, even though there are no other functions in the while loop, you notice there is a constant delay between each reading. Dig through the python library to find out why there is a constant delay. What is the delay amount? In addition, what communication protocol does the Raspberry Pi use to communicate with the Atmega328P on the GrovePi when it tries to read the ultrasonic ranger output using the `grovepi` python library?

From `Software/Python/grovepi.py`:
```python
# Read value from Grove Ultrasonic
def ultrasonicRead(pin):
	write_i2c_block(address, uRead_cmd + [pin, unused, unused])
	time.sleep(.06)	#firmware has a time of 50ms so wait for more than that
	read_i2c_byte(address)
	number = read_i2c_block(address)
	return (number[1] * 256 + number[2])
```

There is a 0.06-second sleep to wait for the hardware.

It uses the I2C protocol.