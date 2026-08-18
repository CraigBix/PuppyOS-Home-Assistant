---
layout: default
title: PuppyOS for Home Assistant
description: Home Assistant puppy feeding tracker, dog feeding automation, toilet reminders, garden gate safety and pet-care dashboards for busy households.
---

# 🐾 PuppyOS for Home Assistant

## Home Assistant puppy feeding tracker, dog feeding automation and pet-care dashboard

PuppyOS is an open-source Home Assistant project for puppy and dog care. It uses ordinary contact sensors, helpers, automations and dashboards to reduce repetitive pet-care admin in shared or busy households.

The core idea is simple:

> **Don't remember to record things. Make your house record them for you.**

## What PuppyOS can do

- Automatically record Breakfast, Lunch and Dinner when the food container opens
- Warn if someone tries to feed the puppy again too soon
- Announce missed meal reminders through a smart speaker
- Track the last garden or toilet break
- Warn if the garden gate is open when outside access is opened
- Display puppy weight, vaccinations, treatments and microchip information
- Show a puppy camera feed in Home Assistant
- Provide separate mobile and desktop/tablet dashboards

## See PuppyOS in action

![PuppyOS mobile Home Assistant puppy dashboard](images/New%20Puppy%20Dashboard%20Image.png)

The feeding tracker can use a small contact sensor attached to the puppy food container:

![Contact sensor on puppy food container](images/Dog_Feeding_Container_with_Sensor.jpeg)

## Start here

- **[Installation and Setup Guide](setup-guide.md)**
- **[Hardware Guide](hardware.md)**
- **[Mobile Dashboard YAML](dashboards/puppyos-mobile.yaml)**
- **[Desktop / Tablet Dashboard YAML](dashboards/puppyos-desktop.yaml)**
- **[Feeding Automation](automations/feeding.yaml)**
- **[Missed Meal Reminders](automations/meal-reminders.yaml)**
- **[Garden Gate Safety](automations/gate-safety.yaml)**

## Who is PuppyOS for?

PuppyOS may be useful for people searching for a Home Assistant puppy feeding tracker, Home Assistant dog feeding automation, smart-home puppy reminder, pet-care dashboard, shared-household dog feeding reminder, or an ADHD-friendly way to reduce repetitive pet-care tracking.

It is designed to remove manual logging where a sensor can observe the real-world action instead.

## Safety

PuppyOS is a convenience and reminder project. It is not a replacement for responsible pet supervision, veterinary advice, secure fencing, correct feeding guidance or medication instructions.

## Open source

PuppyOS is released under the **MIT License**. You can use, modify and adapt it for your own Home Assistant setup.

**[View the full project README](README.md)**
