from flask import Flask
import getpass
import datetime
import pytz
import subprocess

app = Flask(__name__)

@app.route('/htop')
def htop():
    full_name = "Ramesh Kumar"  # Replace with your full name
    username = getpass.getuser()
    ist_time = datetime.datetime.now(pytz.timezone("Asia/Kolkata"))
    
    # Get top output (only top 20 lines for brevity)
    top_output = subprocess.getoutput("top -b -n 1 | head -20")
    top_output = top_output.replace("\n", "<br>")

    return f"""
    <h2>Name: {full_name}</h2>
    <h3>User: {username}</h3>
    <h3>Server Time (IST): {ist_time}</h3>
    <h3>TOP Output:</h3>
    <pre>{top_output}</pre>
    """

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
