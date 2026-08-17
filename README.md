# 🐾 PuppyOS for Home Assistant

### Smart-home automation for puppies, busy households and forgetful humans.

> **Don't remember to record things. Make your house record them for you.**

PuppyOS is a collection of Home Assistant automations and dashboards designed to reduce the everyday mental load of looking after a puppy.

It started with one very ordinary question:

> **"Has someone already fed the puppy?"**

From there came a simple idea: if the house can reliably observe an everyday action, don't make a human remember to log it.

PuppyOS can track feeding, help prevent accidental double-feeding, remind you about missed meals and toilet breaks, warn when a garden gate is open, and bring useful puppy information together in Home Assistant.

---

# 🐶 What PuppyOS Does

## 🍽️ Automatic Feeding Tracking

Put a small contact sensor on the puppy food container. When the container opens, PuppyOS can automatically record:

- Breakfast
- Lunch
- Dinner
- Last feeding time
- Last meal

No app to open. No button to press. No spreadsheet to update.

**Feed the puppy normally and the house records it.**

## 🚨 Double-Feeding Protection

If the food container is opened again too soon after a recorded meal, PuppyOS can announce through a smart speaker:

> **The puppy has already been fed. Please don't feed them again yet.**

The example configuration uses a **150-minute minimum interval**, which you can change for your own feeding schedule.

## ⏰ Missed Meal Reminders

The example three-meal configuration checks for:

| Meal | Reminder |
|---|---:|
| Breakfast | 10:30 |
| Lunch | 15:00 |
| Dinner | 19:30 |

If the expected meal has not been recorded, PuppyOS can announce a reminder. All times are configurable.

## 🚪 Toilet / Garden Tracking

A contact sensor on the garden access door lets PuppyOS record when outside access ends. The dashboard can then show:

- How long ago the puppy last had garden access
- How long remains until the next suggested toilet break
- Whether the garden door is currently open

The example configuration uses a **two-hour reminder period**.

## ⚠️ Garden Gate Safety

PuppyOS can combine two ordinary contact sensors:

```text
Garden access door opens
+
Garden gate is already open
=
WARNING
```

A smart speaker can immediately announce that the gate is open. This is an extra layer of protection, not a replacement for proper supervision or a secure garden.

## ⚖️ Weight, Vaccinations & Treatments

The dashboards can also display information such as:

- Puppy weight and last weighed date
- Last and next vaccination
- Vaccination details
- Parasite treatment
- Last and next treatment dates
- Microchip information

PuppyOS does **not** calculate veterinary medication doses. Always follow your vet's advice and the instructions supplied with veterinary medicines.

## 📹 Puppy Camera

If you already have a Home Assistant-compatible camera, PuppyOS can include its live feed on the dashboard. A camera is completely optional.

---

# 📊 Dashboards

PuppyOS includes **two dashboard layouts** using the same helpers, sensors and automations.

## 📱 Mobile Dashboard

Designed for quick checks on a phone. It prioritises:

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

![PuppyOS Mobile Dashboard](images/New%20Puppy%20Dashboard%20Image.png)

## 🖥️ Desktop / Tablet Dashboard

Designed for larger screens, tablets and wall displays. It includes:

- Multi-column control-centre layout
- Larger puppy photo
- Meal tracking
- Outside and safety status
- Larger live camera
- Weight history graph
- Vaccinations
- Treatment information
- Microchip information

👉 [View the Desktop / Tablet Dashboard YAML](dashboards/puppyos-desktop.yaml)

You can install the mobile dashboard, desktop/tablet dashboard, both, or neither if you only want the automations.

The dashboard should mostly **report what the house has already observed**, rather than becoming another system you have to remember to maintain.

---

# 🏠 Automatic Feeding Detection

The clever bit is deliberately simple: the puppy's normal food container **is the button**.

![PuppyOS Food Container Sensor](images/Dog_Feeding_Container_with_Sensor.jpeg)

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

Nobody needs to remember to interact with PuppyOS before or after feeding.

---

# 🛠️ What You Need

## Minimum Setup

- Home Assistant
- A contact sensor for the puppy food container
- A contact sensor for the garden access door

For gate safety:

- A contact sensor for the garden / side gate

For spoken alerts:

- A Home Assistant-compatible speaker
- A configured TTS service

Everything else is optional.

For more hardware information, see the **[PuppyOS Hardware Guide](hardware.md)**.

---

# ⭐ Recommended Food Container Sensor

The original PuppyOS setup uses a small **Aqara Door & Window Sensor** on the food container. Its compact size makes this type of sensor particularly convenient for attaching to a food tub and lid.

**UK Amazon:** [View the Aqara sensor on Amazon](https://link.amazon/B0j8tTizM)

> **Affiliate disclosure:** The link above is an affiliate link. If you purchase through it, the PuppyOS project may receive a small commission at no additional cost to you.

PuppyOS does **not** require Aqara. You can use any suitable contact sensor that Home Assistant exposes as a `binary_sensor`.

Depending on the Aqara model and your existing smart-home setup, additional compatible hub, Zigbee, Matter or Thread hardware may be required. Check compatibility with your Home Assistant installation before purchasing.

---

# 🚀 Getting Started

If you're new to Home Assistant, use the step-by-step guide:

### 👉 [Read the PuppyOS Setup Guide](setup-guide.md)

Recommended order:

1. Create the required Home Assistant Helpers
2. Identify your contact sensor entity IDs
3. Install the feeding tracker
4. Test food-container detection
5. Install meal reminders
6. Install outside tracking
7. Install the toilet reminder
8. Install gate safety
9. Test everything
10. Add your chosen dashboard

---

# 🤖 Automations

| Module | What it does |
|---|---|
| [Feeding Tracker](automations/feeding.yaml) | Records meals from the food-container sensor and provides double-feeding protection |
| [Missed Meal Reminders](automations/meal-reminders.yaml) | Checks whether expected meals have been recorded |
| [Outside Tracking](automations/toilet-reminder.yaml) | Records when garden access ends |
| [Toilet Reminder](automations/toilet-reminder-alert.yaml) | Reminds the household after the configured period without garden access |
| [Garden Gate Safety](automations/gate-safety.yaml) | Warns when the garden access door opens while the gate is already open |

---

# 🔧 Example Entity IDs

The public YAML uses obvious placeholders such as:

```yaml
binary_sensor.your_food_container_contact
binary_sensor.your_back_door_contact
binary_sensor.your_garden_gate_contact

media_player.your_speaker
camera.your_puppy_camera
```

Replace these with entities from your own Home Assistant installation.

Helpers use examples such as:

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

The complete helper list and creation instructions are in the **[Setup Guide](setup-guide.md)**.

---

# 🧩 Dashboard Requirements

The example dashboards use several Home Assistant custom cards:

- Mushroom Cards
- Button Card
- Advanced Camera Card
- Card Mod

These are commonly installed through HACS.

The PuppyOS automations themselves do **not** require either dashboard.

---

# 🐕 Three Meals Today, Two Meals Later

The initial PuppyOS feeding system is designed around a young puppy eating **three meals per day**.

As feeding requirements change, the automation can be adapted for two meals per day. Always base your puppy's actual feeding schedule and quantity on appropriate veterinary or food-manufacturer guidance rather than the example PuppyOS timings.

---

# 🧠 Why Build This?

Puppy care contains lots of small repetitive tasks. Each one is easy. Remembering all of them while also dealing with work, family, appointments, sleep deprivation and normal life is where things become harder.

This can be especially useful for people who find repetitive tracking or prospective-memory tasks difficult, including some people with ADHD.

PuppyOS is not an ADHD treatment or medical product. It simply applies a useful home-automation principle:

> **If a sensor can reliably observe an everyday action, don't make a human remember to log it.**

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

The public PuppyOS files deliberately use generic placeholders instead of private details from the original installation.

---

# ⚠️ Safety

PuppyOS is a convenience, organisation and reminder project.

It is **not** a replacement for responsible pet supervision, veterinary advice, secure fencing and gates, correct feeding guidance, correct medication instructions or training.

Smart-home devices can fail. Batteries go flat. Wi-Fi disappears at precisely the moment it considers funniest.

Always physically verify anything important to your puppy's health or safety.

---

# 🐾 The Story Behind PuppyOS

PuppyOS started with **Duke**, a new puppy joining a busy household.

The original problem wasn't particularly technical:

> **"Has Duke been fed?"**

Two people could both assume the other person had done it, or both could feed him. A simple contact sensor on the food container solved the logging problem without asking anybody to change how they fed the puppy.

That led to another question: when was he last outside? Then: what if the side gate is open?

And, inevitably, a small feeding sensor became an increasingly elaborate puppy control centre.

PuppyOS is the generic, privacy-safe version of that system, shared so other households can build their own without starting from scratch.

---

# 🤝 Contributing

PuppyOS is an early project and suggestions are welcome. If you improve an automation, find a bug, support different hardware, simplify something or create a better dashboard card, please consider opening an Issue or Pull Request.

---

# 💡 Ideas for Future Versions

- Two-meal feeding mode
- Puppy growth charts
- Medication and vaccination reminders
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

Some hardware links may be affiliate links. These will always be clearly identified. Using an affiliate link may provide a small commission to support the project without increasing the price you pay.

---

# 📜 License

PuppyOS is open-source software released under the **MIT License**.

You are free to use, copy, modify and redistribute PuppyOS, including adapting it for your own puppy, household or Home Assistant setup.

See the full **[MIT License](LICENSE)** for details.

---

## 🐾 PuppyOS

**Less remembering. More puppy.**
