from flask import Flask, request, jsonify

app = Flask(__name__)

# Simulated database
users = {"user1": {"name": "Alice", "location": "Street 5"}}
guardians = {"guardian1": {"name": "Bob", "location": "Street 6"}}

# Send alert endpoint
@app.route('/send_alert', methods=['POST'])
def send_alert():
    data = request.json
    user = data.get('user')
    alert_message = f"Emergency alert from {users[user]['name']} at {users[user]['location']}!"
    
    # Notify all guardians
    for g in guardians.values():
        print(f"Notification sent to {g['name']}: {alert_message}")
    
    return jsonify({"status": "Alert sent!", "message": alert_message})

if __name__ == '__main__':
    app.run(debug=True)
