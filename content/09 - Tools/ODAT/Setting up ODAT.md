```bash
sudo apt-get install -y build-essential python3-dev libaio1 
cd ~ 
wget https://files.pythonhosted.org/packages/source/c/cx_Oracle/cx_Oracle-8.3.0.tar.gz tar xzf cx_Oracle-8.3.0.tar.gz 
cd cx_Oracle-8.3.0 python3 setup.py build 
sudo python3 setup.py install 
cd ~ 
git clone https://github.com/quentinhardy/odat.git 
cd odat/ pip install python-libnmap 
git submodule init 
git submodule update 
sudo apt-get install python3-scapy -y 

sudo pip3 install colorlog termcolor passlib python-libnmap 
sudo apt-get install build-essential libgmp-dev -y 
pip3 install pycryptodome 
pip3 install openpyxl
```

## Testing ODAT if its working
```bash
./odat.py -h
```
