# Anaconda
WIth VS code
```
conda install -c anaconda ipykernel
```
Setup python interpreter
```
python -m ipykernel install --user --name=<venv>
```

Add new environment
```
conda create --name myName
# export packages
conda list --export > packages.txt
# install packages
conda install --file packages.txt

```

To avoid activates in the terminal 
```setting.json
"python.terminal.activateEnvironment": false
```
# Python

create venv
```
python -m venv myenv
```
activate
```
myenv\Scripts\activate
```
export 
```
pip freeze > requirements.txt
```
install env
```
pip install -r requirements.txt
```