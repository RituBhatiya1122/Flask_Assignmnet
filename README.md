# Flask_Assignmnet
from flask import Flask, request, render_template
from pymongo import MongoClient

app = Flask(__name__)

# Replace with your MongoDB Atlas URI
client = MongoClient("YOUR_MONGODB_ATLAS_URI")
db = client["myDatabase"]
collection = db["myCollection"]

@app.route("/")
def index():
    return render_template("form.html")

@app.route("/submit", methods=["POST"])
def submit():
    name = request.form["name"]
    age = request.form["age"]
    collection.insert_one({"name": name, "age": age})
    return "Data submitted successfully"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=81)
<!DOCTYPE html>
<html>
  <body>
    <h2>Form</h2>
    <form method="POST" action="/submit">
      <input type="text" name="name" placeholder="Name" required><br><br>
      <input type="number" name="age" placeholder="Age" required><br><br>
      <button type="submit">Submit</button>
    </form>
  </body>
</html>

3.mongodb+srv://bhatiyaritu1122:9ZIuxGY6o7y561Xa@cluster0.dsgrpla.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0”
