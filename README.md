# physical-therapy
An Ai powered web application that generates personalized exercise plans for physical therapy based on patient history, medical condition, and fitness goals.
app = Flask(_name_)

def generate_exercise_plan(patient_info):
    age = patient_info['age']
    condition = patient_info['condition']
    goal = patient_info['goal']
    activity_level = patient_info['activity_level']

    plan = {"aerobic": "", "strength": "", "flexibility": ""}

    if condition == "hypertension":
        plan["aerobic"] = "30 minutes brisk walking 5 days/week"
        plan["strength"] = "Light resistance training 2 days/week"
    elif condition == "arthritis":
        plan["aerobic"] = "Low-impact activities like swimming or cycling 3-4 days/week"
        plan["flexibility"] = "Daily joint mobility exercises"
    elif condition == "diabetes":
        plan["aerobic"] = "Moderate-intensity aerobic exercise 5 days/week"
        plan["strength"] = "Full-body strength training 2-3 days/week"

    if activity_level == "sedentary":
        plan["aerobic"] = "Start with 10-15 minutes/day and increase gradually"

    if goal == "weight loss":
        plan["aerobic"] += "; include HIIT 1-2 times/week if possible"
    elif goal == "rehabilitation":
        plan["aerobic"] = "Therapist-supervised sessions only"
        plan["strength"] = "Functional bodyweight exercises under supervision"

    return plan

@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        patient_info = {
            'age': int(request.form['age']),
            'condition': request.form['condition'],
            'goal': request.form['goal'],
            'activity_level': request.form['activity_level']
        }
        plan = generate_exercise_plan(patient_info)
        return render_template('index.html', plan=plan, patient=patient_info)
    return render_template('index.html')

if _name_ == '_main_':
    app.run(debug=True)
