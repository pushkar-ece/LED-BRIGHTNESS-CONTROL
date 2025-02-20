import matplotlib.pyplot as plt
import numpy as np

def draw_led(brightness):
    plt.clf()
    plt.xlim(-1.2, 1.2)
    plt.ylim(-1.2, 1.2)

    rgb = (0.0, 0.8, 1.0)
    led_color = (rgb[0] * brightness, rgb[1] * brightness, rgb[2] * brightness)

    for i in np.linspace(0.5, 0.9, 5):
        glow = plt.Circle((0, 0), i, color=led_color, alpha=0.2 * (i / 0.9))
        plt.gca().add_patch(glow)

    circle = plt.Circle((0, 0), 0.4, color=led_color, edgecolor='black', linewidth=2)
    plt.gca().add_patch(circle)

    plt.text(0, -0.8, f'Brightness: {brightness*100:.0f}%', fontsize=12, ha='center', color='black', fontweight='bold')
    plt.axis('off')
    plt.pause(0.1)

def main():
    plt.ion()
    brightness = 0.5

    draw_led(brightness)
    print("Press '+' to increase brightness, '-' to decrease, 'q' to quit.")

    while True:
        user_input = input("Enter command (+/-/q): ").strip().lower()

        if user_input == '+':
            brightness = min(1.0, brightness + 0.1)
        elif user_input == '-':
            brightness = max(0.0, brightness - 0.1)
        elif user_input == 'q':
            break

        draw_led(brightness)

    plt.ioff()
    plt.show()

if __name__ == "__main__":
    main()
