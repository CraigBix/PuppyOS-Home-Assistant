# 🐾 PuppyOS for Home Assistant

### Smart-home automation for puppies, busy households and forgetful humans.

> **Don't remember to record things. Make your house record them for you.**

PuppyOS is a collection of Home Assistant automations and dashboard components designed to reduce the everyday mental load of looking after a puppy.

It started with a very ordinary problem:

> **"Has someone already fed the puppy?"**

In a household where more than one person looks after a dog, surprisingly simple questions can become difficult:

- Has he had breakfast?
- When was he last fed?
- Has somebody else already fed him?
- When did he last go outside?
- Is the garden gate shut?
- When is his next vaccination?
- When did we last give his parasite treatment?
- What did he weigh last time?
- Where are the insurance details when we actually need them?

PuppyOS lets **Home Assistant answer those questions for you**.

---

# 🐶 What PuppyOS Does

PuppyOS currently includes:

### 🍽️ Automatic Feeding Tracking

Put a small contact sensor on the puppy food container.

When the container opens, PuppyOS can automatically record:

- Breakfast
- Lunch
- Dinner
- Last feeding time
- Last meal

No phone app to open.

No button to press.

No spreadsheet to remember to update.

**Feed the puppy normally and the house records it.**

---

### 🚨 Double-Feeding Protection

If somebody opens the food container again too soon after a recorded meal, PuppyOS can announce through a smart speaker:

> **The puppy has already been fed. Please don't feed them again yet.**

This is particularly useful in households where more than one person shares feeding duties.

The example configuration uses a **150-minute minimum interval**, which can be changed to suit your own feeding schedule.

---

### ⏰ Missed Meal Reminders

The example three-meal configuration checks for:

| Meal | Reminder |
|---|---:|
| Breakfast | 10:30 |
| Lunch | 15:00 |
| Dinner | 19:30 |

If the expected meal has not been recorded, PuppyOS can announce that the puppy needs feeding.

The times are completely configurable.

---

### 🚪 Toilet / Garden Tracking

A contact sensor on the garden access door lets PuppyOS record when outside access ends.

The dashboard can then show:

- How long ago the puppy last had garden access
- How long remains until the next suggested toilet break
- Whether the garden door is currently open

The example configuration uses a **two-hour reminder period**.

---

### ⚠️ Garden Gate Safety

PuppyOS can combine two ordinary contact sensors to create a useful safety system.

```text
Garden access door opens
+
Garden gate is already open
=
WARNING
```

A smart speaker can immediately announce:

> **Warning. The garden gate is open. Please close the gate before letting the puppy outside.**

This does not replace proper supervision or a secure garden, but it provides another useful layer of protection.

---

### ⚖️ Puppy Weight Tracking

Record your puppy's current weight and the date they were weighed.

Because Home Assistant keeps entity history, this can also provide the foundation for a puppy growth graph.

This becomes particularly useful while a puppy is growing rapidly.

---

### 💉 Vaccinations & Treatments

The dashboard can keep important health information together, including:

- Last vaccination
- Next vaccination
- Vaccination details
- Parasite treatment
- Treatment dose
- Last treatment date
- Next treatment date

PuppyOS does **not** calculate veterinary medication doses.

Always follow your vet's advice and the instructions supplied with veterinary medicines.

---

### 🏥 Vet, Microchip & Insurance Information

The dashboard can provide quick access to:

- Veterinary practice details
- Vet telephone number
- Microchip information
- Insurance details
- Insurance documents

Instead of hunting through emails or paperwork when something happens, important information can be available from the same puppy dashboard.

---

### 📹 Puppy Camera

If you already have a Home Assistant-compatible camera, PuppyOS can include its live feed directly on the dashboard.

A camera is completely optional.

---

# 📱 The PuppyOS Dashboard

# 📊 Dashboards

PuppyOS now includes two dashboard layouts using the same helpers, sensors and automations.

Choose the one that best fits where you use Home Assistant.

## 📱 Mobile Dashboard

Designed for quick checks on a phone.

Prioritises:

- Breakfast / Lunch / Dinner
- Last fed
- Food container
- Last outside
- Toilet status
- Garden gate
- Back door
- Weight
- Vaccinations
- Treatments
- Microchip
- Puppy camera

👉 [View the Mobile Dashboard YAML](dashboards/puppyos-mobile.yaml)

---

## 🖥️ Desktop / Tablet Dashboard

Designed for larger screens, tablets and wall displays.

Includes:

- Three-column control-centre layout
- Larger puppy photo
- Meal tracking
- Outside and safety status
- Larger live camera
- Weight history graph
- Vaccinations
- Treatment information
- Microchip
- Vet / insurance / document shortcuts

👉 [View the Desktop / Tablet Dashboard YAML](dashboards/puppyos-desktop.yaml)

---

Both dashboards use the same PuppyOS automations.

You can install:

- Mobile only
- Desktop / tablet only
- Both
- Neither, if you only want the automations

Here's an example of PuppyOS running as a mobile Home Assistant dashboard:

![PuppyOS Mobile Dashboard](images/New%20Puppy%20Dashboard%20Image.png)

The dashboard brings feeding, outside access, safety, weight, vaccinations, parasite treatments and other puppy information together in one place.

## Automatic Feeding Detection

The clever bit is surprisingly simple: a small contact sensor attached to the puppy's food container.

![PuppyOS Food Container Sensor](images/Dog_Feeding_Container_with_Sensor.jpeg)

When the container is opened, Home Assistant detects it automatically. PuppyOS can then record the meal, update the dashboard and warn another household member if they try to feed the puppy again too soon.

**No buttons. No manual logging. Just feed the puppy.**

The supplied dashboard is designed to work particularly well on a phone.

It can show at a glance:

```text
🐾 PUPPY

Outside & Safety
├── Last Outside
├── Toilet Status
├── Garden Gate
└── Back Door

Food
├── Breakfast
├── Lunch
├── Dinner
├── Last Fed
└── Food Container

Health
├── Weight
├── Vaccinations
├── Treatments
└── Microchip

Information
├── Vet
├── Insurance
└── Documents

Camera
└── Live Puppy Cam
```

The idea is not to create another system that needs constant administration.

The dashboard should mostly **report what the house has already observed**.

---

# 🧠 Why Build This?

Puppy care contains lots of small repetitive tasks.

Each one is easy.

Remembering **all of them**, while also dealing with work, children, appointments, sleep deprivation and normal life, is where things become harder.

This can be especially useful for people who find repetitive tracking or prospective-memory tasks difficult, including some people with ADHD (like me!)

PuppyOS is not an ADHD treatment or medical product.

It simply applies a useful home-automation principle:

> **If a sensor can reliably observe an everyday action, don't make a human remember to log it.**

That principle works whether your household is neurodivergent, extremely busy, wonderfully chaotic, or simply tired because somebody brought home a puppy.

---

# 🏠 How Feeding Detection Works

There is deliberately no special PuppyOS feeding button.

The puppy's normal food container **is the button**.

A small contact sensor detects the lid opening.

```text
          FOOD CONTAINER
                │
                ▼
        Contact sensor opens
                │
                ▼
          Home Assistant
                │
       ┌────────┴────────┐
       ▼                 ▼
  Record meal      Check last feed
       │                 │
       ▼                 ▼
  Update dashboard   Too soon?
                         │
                         ▼
                    Speaker warning
```

This is what makes the system useful in everyday life.

Nobody needs to remember to interact with PuppyOS before or after feeding.

---

# 🛠️ What You Need

## Minimum Setup

You will need:

- Home Assistant
- A contact sensor for the puppy food container
- A contact sensor for the garden access door

For gate safety:

- A contact sensor for the garden / side gate

For spoken alerts:

- A Home Assistant-compatible speaker
- A configured TTS service

Everything else is optional.

---

# ⭐ Recommended Food Container Sensor

The original PuppyOS setup uses a small **Aqara Door & Window Sensor** on the food container.

Its compact size makes this type of sensor particularly convenient for attaching to a food tub and lid.

**UK Amazon:** [View the Aqara sensor on Amazon](https://link.amazon/B0j8tTizM)

> **Affiliate disclosure:** The link above is an affiliate link. If you purchase through it, the PuppyOS project may receive a small commission at no additional cost to you.

### Important

PuppyOS does **not** require Aqara.

You can use any suitable contact sensor that Home Assistant exposes as a `binary_sensor`.

Depending on the Aqara model you choose and your existing smart-home setup, additional compatible hub, Zigbee, Matter or Thread hardware may be required.

Check compatibility with your Home Assistant installation before purchasing.

---

# 🚀 Getting Started

If you're new to Home Assistant, don't start by copying random bits of YAML and hoping for the best.

Use the setup guide:

### 👉 [Read the PuppyOS Setup Guide](setup-guide.md)

The recommended order is:

1. Create the required Home Assistant Helpers
2. Identify your contact sensor entity IDs
3. Install the feeding tracker
4. Test food-container detection
5. Install meal reminders
6. Install outside tracking
7. Install the toilet reminder
8. Install gate safety
9. Test everything
10. Add the dashboard

---

# 🤖 Automations

The current PuppyOS automation modules are:

### 🍽️ Feeding Tracker

[View `feeding.yaml`](automations/feeding.yaml)

Automatically records Breakfast, Lunch and Dinner from the food-container contact sensor and provides double-feeding protection.

---

### ⏰ Missed Meal Reminders

[View `meal-reminders.yaml`](automations/meal-reminders.yaml)

Checks whether expected meals have been recorded and can announce reminders through a smart speaker.

---

### 🚪 Outside Tracking

[View `toilet-reminder.yaml`](automations/toilet-reminder.yaml)

Records when garden access ends.

---

### 🚽 Toilet Reminder

[View `toilet-reminder-alert.yaml`](automations/toilet-reminder-alert.yaml)

Provides a reminder after the configured period without garden access.

---

### ⚠️ Garden Gate Safety

[View `gate-safety.yaml`](automations/gate-safety.yaml)

Warns when the puppy's garden access door opens while the garden gate is already open.

---

# 📊 Dashboard

The example dashboard configuration is here:

### 👉 [View the PuppyOS Dashboard YAML](puppy-dashboard.yaml)

The dashboard currently uses several Home Assistant custom cards:

- Mushroom Cards
- Button Card
- Advanced Camera Card
- Card Mod

These are commonly installed using HACS.

The automations themselves do **not** require the dashboard.

---

# 🔧 Example Entity IDs

PuppyOS uses obvious placeholders in the public YAML.

For example:

```yaml
binary_sensor.your_food_container_contact
binary_sensor.your_back_door_contact
binary_sensor.your_garden_gate_contact

media_player.your_speaker
camera.your_puppy_camera
```

Replace these with entities from your own Home Assistant installation.

The Helpers use examples such as:

```yaml
input_datetime.puppy_last_fed
input_datetime.puppy_breakfast_fed
input_datetime.puppy_lunch_fed
input_datetime.puppy_dinner_fed

input_text.puppy_last_meal

input_datetime.puppy_last_outside

input_number.puppy_weight
input_datetime.puppy_last_weighed
```

The full list and creation instructions are in the [Setup Guide](setup-guide.md).

---

# 🐕 Three Meals Today, Two Meals Later

The initial PuppyOS feeding system is designed around a young puppy eating **three meals per day**.

Puppies don't stay puppies forever.

As feeding requirements change, the automation can be adapted for two meals per day.

Always base your puppy's actual feeding schedule and quantity on appropriate veterinary or food-manufacturer guidance rather than the example PuppyOS timings.

---

# 🔐 Privacy

Your Home Assistant configuration may contain much more private information than you realise.

Before publishing your own configuration or screenshots, check for:

- Home addresses
- Insurance policy numbers
- Microchip numbers
- Camera URLs
- Network information
- Alarm entities
- Device names
- Personal names
- Private documents

The public PuppyOS files deliberately use generic placeholders instead of details from the original installation.

---

# ⚠️ Safety

PuppyOS is a convenience, organisation and reminder project.

It is **not** a replacement for:

- Responsible pet supervision
- Veterinary advice
- Secure fencing and gates
- Correct feeding guidance
- Correct medication instructions
- Training
- Common sense

Smart-home devices can fail.

Batteries go flat.

Wi-Fi disappears at precisely the moment it considers funniest.

Always physically verify anything important to your puppy's health or safety.

---

# 🐾 The Story Behind PuppyOS

PuppyOS started with **Duke**, a new puppy joining a busy household.

The original problem wasn't particularly technical:

> **"Has Duke been fed?"**

Two people could both assume the other person had done it.

Or both could feed him.

A simple contact sensor on the food container solved the logging problem without asking anybody to change how they fed the puppy.

That led to another question:

> When was he last outside?

Then:

> What if the side gate is open?

And, inevitably, a small feeding sensor became an increasingly elaborate puppy control centre.

PuppyOS is the generic, privacy-safe version of that system.

The goal is to share the useful bits so other households can build their own version without starting from scratch.

---

# 🤝 Contributing

PuppyOS is an early project and suggestions are welcome.

If you:

- Improve an automation
- Find a bug
- Support different hardware
- Adapt PuppyOS for two meals per day
- Create a better dashboard card
- Find a simpler way of doing something

please consider opening an Issue or Pull Request.

This project should become better through real households actually using it.

---

# 💡 Ideas for Future Versions

Possible future additions include:

- Two-meal feeding mode
- Puppy growth charts
- Weight history
- Medication reminders
- Vaccination reminders
- Walk tracking
- Training logs
- Grooming reminders
- Multiple-dog support
- Mobile notifications
- Better dashboard themes
- Optional Blueprints for easier installation

---

# 🤖 Built With a Little AI Assistance

PuppyOS was conceived, built and tested around a real puppy and a real Home Assistant installation.

ChatGPT from OpenAI helped turn the ideas into Home Assistant YAML, debug the automations, structure the documentation and convert the original Duke-specific setup into the generic PuppyOS project.

Duke's contribution consisted primarily of eating, going outside and generating requirements.

His QA methodology remains proprietary.

---

# ❤️ Support PuppyOS

PuppyOS is shared freely for other Home Assistant and puppy-owning households to use and adapt.

Some hardware links may be affiliate links. These will always be clearly identified.

Using an affiliate link may provide a small commission to support the project without increasing the price you pay.

---

# 📜 License

A formal open-source license will be added to the repository.

Until then, please do not assume that the absence of a license grants unrestricted reuse or redistribution rights.

---

## 🐾 PuppyOS

**Less remembering. More puppy.**
