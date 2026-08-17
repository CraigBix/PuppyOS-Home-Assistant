# PuppyOS Setup Guide

PuppyOS is a collection of Home Assistant automations and dashboard cards designed to reduce the mental load of looking after a puppy in a busy household.

The idea is simple:

> Don't remember to record things. Let the house record them for you.

PuppyOS can help track:

- Feeding
- Breakfast, lunch and dinner
- Accidental double-feeding
- Missed meals
- Toilet / garden breaks
- Garden gate safety
- Weight
- Vaccinations
- Flea / tick / worming treatments
- Microchip information
- Vet details
- Insurance information
- Puppy cameras

You do **not** need every feature.

Start with the bits that are useful to your household and add more later.

---

# 1. What You Need

At minimum, PuppyOS needs:

- Home Assistant
- A contact sensor on the puppy food container
- A contact sensor on the door used to access the garden

For the garden gate safety automation you will also need:

- A contact sensor on the garden / side gate

For spoken announcements you will need:

- A media player supported by Home Assistant
- A working Home Assistant TTS service

Examples include:

- Sonos
- Google / Nest speakers
- Other Home Assistant compatible media players

### Recommended Food Container Sensor

We use a small **Aqara Door & Window Sensor** on the puppy food container.

It's particularly well suited to this job because the sensor is tiny, battery powered and simply sticks to the food container and lid. Opening the lid changes the contact state, which PuppyOS uses to detect a feeding event.

**Recommended:** Aqara Door & Window Sensor  
**UK Amazon:** [View on Amazon](https://link.amazon/B0j8tTizM)

> **Affiliate disclosure:** This is an affiliate link. If you buy through it, the PuppyOS project may receive a small commission at no additional cost to you.

**Important:** The standard Zigbee Aqara Door & Window Sensor requires a compatible Aqara hub. If you don't already use Aqara, you can use any Home Assistant-compatible contact sensor instead.

PuppyOS does not require Aqara specifically. All it needs is a contact sensor that appears in Home Assistant as a `binary_sensor`.

# 2. Optional Hardware

PuppyOS can also make use of:

- Zigbee contact sensors
- Matter contact sensors
- Wi-Fi contact sensors
- Cameras
- Pet detection cameras
- Temperature sensors
- Smart speakers
- Presence sensors

The food tracking system only needs a simple contact sensor fitted to the food container lid.

When the food container opens, PuppyOS assumes that the puppy is being fed.

---

# 3. Dashboard Requirements

The example PuppyOS dashboard uses several custom Home Assistant cards.

These can normally be installed through HACS.

The dashboard currently uses:

- Mushroom Cards
- Button Card
- Advanced Camera Card
- Card Mod

If you do not want to install these, you can still use all of the PuppyOS automations without the supplied dashboard.

---

# 4. Required Helpers

Home Assistant Helpers act as PuppyOS's little database.

Create them from:

**Settings → Devices & Services → Helpers → Create Helper**

## Feeding Helpers

Create four **Date and Time** helpers:

```text
Puppy Last Fed
Puppy Breakfast Fed
Puppy Lunch Fed
Puppy Dinner Fed
```

Example entity IDs:

```text
input_datetime.puppy_last_fed
input_datetime.puppy_breakfast_fed
input_datetime.puppy_lunch_fed
input_datetime.puppy_dinner_fed
```

Create one **Text** helper:

```text
Puppy Last Meal
```

Example:

```text
input_text.puppy_last_meal
```

---

# 5. Toilet / Garden Helper

Create one **Date and Time** helper:

```text
Puppy Last Outside
```

Example:

```text
input_datetime.puppy_last_outside
```

PuppyOS records the time when the garden access door closes.

This is intentional.

If the door is left open, the puppy still has access to the garden, so a toilet reminder is unnecessary.

Once the door closes, the toilet reminder clock begins.

---

# 6. Weight Helpers

Create one **Number** helper:

```text
Puppy Weight
```

Suggested settings:

```text
Minimum: 0
Maximum: 50
Step: 0.1
Unit: kg
Display mode: Input field
```

Example entity:

```text
input_number.puppy_weight
```

Create one **Date and Time** helper:

```text
Puppy Last Weighed
```

Example:

```text
input_datetime.puppy_last_weighed
```

Only change the weight helper when the puppy is actually weighed.

Home Assistant history can then be used to create a puppy growth graph.

---

# 7. Vaccination Helpers

Create two **Date and Time** helpers:

```text
Puppy Last Vaccination
Puppy Next Vaccination
```

Example entities:

```text
input_datetime.puppy_last_vaccination
input_datetime.puppy_next_vaccination
```

Create one **Text** helper:

```text
Puppy Last Vaccination Details
```

Example:

```text
input_text.puppy_last_vaccination_details
```

This can contain something such as:

```text
Nobivac DHP + L4
```

---

# 8. Parasite Treatment Helpers

Create two **Text** helpers:

```text
Puppy Parasite Treatment
Puppy Parasite Dose
```

Example entities:

```text
input_text.puppy_parasite_treatment
input_text.puppy_parasite_dose
```

Create two **Date and Time** helpers:

```text
Puppy Last Parasite Treatment
Puppy Next Parasite Treatment
```

Example entities:

```text
input_datetime.puppy_last_parasite_treatment
input_datetime.puppy_next_parasite_treatment
```

Use the product name, dose and treatment frequency recommended by your vet or shown on the veterinary product instructions.

Do not use PuppyOS to calculate medication doses.

---

# 9. Microchip Helper

Create one **Text** helper:

```text
Puppy Microchip
```

Example:

```text
input_text.puppy_microchip
```

Enter your puppy's microchip number as the helper value.

For privacy, the example dashboard does not display the full microchip number permanently.

It can be viewed by tapping the Microchip card.

---

# 10. Rename Your Sensors

The example YAML contains placeholder entities.

You MUST replace these with entities from your own Home Assistant installation.

## Food Container

Example placeholder:

```text
binary_sensor.your_food_container_contact
```

Replace it with your contact sensor.

## Garden Access Door

Example placeholder:

```text
binary_sensor.your_back_door_contact
```

Replace it with the contact sensor on the door used to let your puppy outside.

## Garden Gate

Example placeholder:

```text
binary_sensor.your_garden_gate_contact
```

Replace it with your gate contact sensor.

## Speaker

Example placeholder:

```text
media_player.your_speaker
```

Replace it with the media player you want PuppyOS announcements to use.

## Camera

Example placeholder:

```text
camera.your_puppy_camera
```

Replace it with your puppy camera entity.

---

# 11. Feeding Logic

The supplied feeding automation assumes a puppy is currently eating three meals per day.

The logic is:

```text
First valid food-container opening today
→ Breakfast

Second valid opening
→ Lunch

Third valid opening
→ Dinner
```

The automation also remembers:

```text
Last Fed
Last Meal
```

This allows the dashboard to display information such as:

```text
Lunch
1.4 hours ago
```

---

# 12. Double-Feeding Protection

The example feeding automation uses a minimum interval of:

```text
150 minutes
```

If the food container is opened again within that period, PuppyOS can announce:

```text
The puppy has already been fed.
Please don't feed them again yet.
```

Importantly, the rejected opening does **not** overwrite the last valid feeding timestamp.

This means PuppyOS remembers the real previous meal rather than treating the accidental opening as another feed.

You can change the 150-minute period to suit your own feeding schedule.

---

# 13. Missed Meal Reminders

The supplied example reminder times are:

```text
Breakfast: 10:30
Lunch:     15:00
Dinner:    19:30
```

At each time PuppyOS checks whether that meal has been recorded today.

If not, a spoken reminder can be sent to your chosen speaker.

These times are examples only.

Change them to match your puppy's feeding schedule.

---

# 14. Toilet Reminder

The example toilet reminder uses a two-hour interval.

When the garden access door closes:

```text
Puppy Last Outside = current time
```

If the door remains closed for two hours, PuppyOS can announce a toilet reminder.

The supplied example only operates between:

```text
10:00
and
22:00
```

This prevents middle-of-the-night announcements.

If the garden door is already open, no reminder is needed because the puppy already has access outside.

---

# 15. Garden Gate Safety

This is one of the most important PuppyOS automations.

The idea is:

```text
Garden access door opens
+
Garden gate is already open
=
WARNING
```

A speaker can immediately announce that the gate is open.

This can reduce the risk of a puppy escaping onto a road or into an unsafe area.

Always test this automation physically after creating it.

Do not assume a safety automation works until you have verified it.

---

# 16. Puppy Photo

The example dashboard expects a puppy image at:

```text
/config/www/puppy.jpg
```

Depending on your Home Assistant installation this may also appear as:

```text
/homeassistant/www/puppy.jpg
```

Home Assistant then serves it as:

```text
/local/puppy.jpg
```

You can replace the filename in the dashboard YAML if you prefer another image.

---

# 17. Vet Details

The example dashboard includes a section for:

- Vet name
- Address
- Telephone number
- Navigation link

Replace all example information with your own veterinary practice.

A mobile-friendly dashboard can make this particularly useful during an emergency.

---

# 18. Insurance Documents

PDF documents can be stored in the Home Assistant `www` directory.

For example:

```text
/config/www/puppy_docs/insurance.pdf
```

Home Assistant can then access that file as:

```text
/local/puppy_docs/insurance.pdf
```

You can create a dashboard button with:

```yaml
type: button
name: Insurance Certificate
icon: mdi:file-certificate-outline
tap_action:
  action: url
  url_path: /local/puppy_docs/insurance.pdf
```

Do not publish your real policy number, home address, microchip number or private insurance documents in a public GitHub repository.

---

# 19. Recommended Installation Order

If you are new to Home Assistant, install PuppyOS in this order:

1. Create the Helpers
2. Identify your contact sensor entity IDs
3. Install the feeding automation
4. Test the food-container sensor
5. Install the meal reminder automation
6. Install the outside tracking automation
7. Install the toilet reminder alert
8. Install the garden gate safety automation
9. Test every automation
10. Install the dashboard
11. Add health / vet / insurance information

---

# 20. Testing

Test every automation individually.

For feeding:

```text
Open food container
→ Breakfast should record
```

For gate safety:

```text
Open garden gate
Open back door
→ Warning should play
```

For outside tracking:

```text
Open back door
Close back door
→ Puppy Last Outside should update
```

Do not wait until an automation is genuinely needed before discovering that an entity ID is wrong.

---

# 21. Three Meals to Two Meals

Many puppies move from three meals per day to two meals as they get older.

The current example is deliberately designed around three meals.

When your puppy changes feeding schedule, update:

- Feeding automation
- Meal reminder automation
- Dashboard meal cards
- Reminder times

A future PuppyOS version may provide separate two-meal and three-meal configurations.

---

# 22. Privacy Before Publishing

If you fork PuppyOS or publish screenshots of your own setup, check carefully for:

- Home address
- Vet address if you consider it private
- Insurance policy numbers
- Microchip numbers
- Camera URLs
- Personal names
- Device names
- Alarm / security entities
- Network details

Home Assistant dashboards can contain far more personal information than they appear to at first glance.

---

# 23. Safety

PuppyOS is intended as a convenience and reminder system.

It is not a replacement for:

- Responsible pet supervision
- Veterinary advice
- Secure fencing and gates
- Correct medication instructions
- Appropriate feeding guidance
- Training

Never rely solely on a smart-home automation for your puppy's safety.

---

# 24. Philosophy

PuppyOS was created around one simple idea:

> Reduce the number of things a household has to remember.

Instead of asking:

```text
Has someone fed the puppy?
```

ask the house.

Instead of wondering:

```text
When did the puppy last go outside?
```

ask the house.

Instead of hoping:

```text
Did somebody leave the gate open?
```

make the house shout about it.

That is PuppyOS.
