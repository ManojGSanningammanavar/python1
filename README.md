# Virtual Pet Simulator game







import random
import time

def main():
    """
    The main function to run the Virtual Pet Simulator game.
    """
    
    # ------------------ Pet Setup ------------------
    # Bonus: Get pet's name from the user
    pet_name = input("Welcome to your Virtual Pet Simulator! What would you like to name your pet? ")
    if not pet_name:
        pet_name = "Buddy" # Default name if none is entered

    pet = {
        "name": pet_name,
        "happiness": 50,
        "hunger": 50
    }
    
    print(f"\nGreat! You've adopted {pet['name']}. Take good care of them! 🐾\n")
    time.sleep(1) # Pause for effect

    # ------------------ Game Loop ------------------
    while True:
        # --- 5. Game Over Conditions ---
        if pet["hunger"] >= 100:
            print(f"\nOh no! {pet['name']} got too hungry and ran away to find food. 😢")
            print("--- GAME OVER ---")
            break
        if pet["happiness"] <= 0:
            print(f"\nOh no! {pet['name']} became too sad and decided to leave. 💔")
            print("--- GAME OVER ---")
            break

        # --- 3. User Menu ---
        print("+" + "-"*25 + "+")
        print("| What do you want to do?   |")
        print("|-------------------------|")
        print("| 1. Feed your pet        |")
        print("| 2. Play with your pet   |")
        print("| 3. Check status         |")
        print("| 4. Quit                 |")
        print("+" + "-"*25 + "+")

        choice = input("Enter your choice (1-4): ")

        # --- 2. Actions ---
        if choice == '1':
            # Feed the pet
            pet["hunger"] -= 25
            pet["happiness"] -= 5 # Feeding is a necessity, not always fun
            print(f"\nYou fed {pet['name']}. Yum! 🍖")
        
        elif choice == '2':
            # Play with the pet
            pet["happiness"] += 20
            pet["hunger"] += 10 # Playing makes the pet hungry
            print(f"\nYou played with {pet['name']}. So much fun! 🎾")

        elif choice == '3':
            # Check Status
            print(f"\n--- {pet['name']}'s Status ---")
            print(f"Happiness: {pet['happiness']}/100")
            print(f"Hunger:    {pet['hunger']}/100")
            # Give a little feedback on status
            if pet['happiness'] < 20:
                print(f"{pet['name']} is looking very sad.")
            if pet['hunger'] > 80:
                print(f"{pet['name']} is starving!")
            print("------------------------")

        elif choice == '4':
            # Quit the game
            print(f"\nGoodbye! Thanks for playing with {pet['name']}. 👋")
            break
        
        else:
            print("\nInvalid choice. Please enter a number between 1 and 4.")
            continue # Skip the time passing part for an invalid choice
        
        # --- 4. Automatic Changes (Time Passing) ---
        pet["hunger"] += 5
        pet["happiness"] -= 5
        print(f"Time passes... {pet['name']} gets a little hungrier and less happy.")

        # --- 1. Pet Status Clamping and Logic ---
        # Ensure levels stay between 0 and 100
        pet["happiness"] = max(0, min(100, pet["happiness"]))
        pet["hunger"] = max(0, min(100, pet["hunger"]))

        # If hunger gets too high, happiness decreases faster
        if pet["hunger"] > 80:
            pet["happiness"] -= 10
            print(f"{pet['name']} is very hungry and getting sad! 😟")
        
        # --- Bonus: Random Events ---
        if random.random() < 0.2: # 20% chance of a random event
            event = random.choice(["found_snack", "got_sick", "saw_squirrel"])
            if event == "found_snack":
                pet["hunger"] -= 15
                pet["happiness"] += 5
                print(f"\n🎉 RANDOM EVENT: {pet['name']} found a hidden snack! Hunger decreased.")
            elif event == "got_sick":
                pet["happiness"] -= 20
                print(f"\n🤒 RANDOM EVENT: Oh no! {pet['name']} feels a bit sick. Happiness decreased.")
            elif event == "saw_squirrel":
                pet["happiness"] += 15
                pet["hunger"] += 5
                print(f"\n🐿️ RANDOM EVENT: {pet['name']} excitedly chased a squirrel! Happiness increased.")

        print("-" * 30) # Separator for the next turn
        time.sleep(1) # Pause to make the game flow better


# This line ensures the main() function runs when the script is executed
if __name__ == "__main__":
    main()
