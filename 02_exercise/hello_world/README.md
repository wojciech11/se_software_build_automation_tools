## Amazing Hello World App

1. Do not forget to use the virtual python env:

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

2. Instal the dependencies:

   ```bash
   pip install -r requirements.txt;
   pip install -r test_requirements.txt;
   ``` 

3. Check whether the app works, start it, and use `curl` to call the app web api:

   ```bash
   PYTHONPATH=. FLASK_APP=hello_world flask run
   ```

   ```bash
   curl 127.0.0.1:5000
   ```

   ```bash
   curl 127.0.0.1:5000/outputs
   ```

   ```bash
   curl '127.0.0.1:5000/?output=json'
   ```

3. What is the code without tests:

   ```bash
   PYTHONPATH=. py.test  --verbose -s
   ```

4. Let's lint our code:

   ```bash
   flake8 hello_world test main.py
   ```

5. Place for your notes:

   ```bash
   ```
