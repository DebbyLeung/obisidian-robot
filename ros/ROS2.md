[Humble installation](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html)
setup source everytime
```
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
```
## create workspace
```shell
sudo apt install python3-rosdep2
rosdep update
rosdep install -i --from-path src --rosdistro humble -y
```

colcon cannot use the most updated setup.py.
```python
pip install --upgrade setuptools==58.2.0
```
# Simulation tool
- [[Webots]]
- [[Gazebo]]



