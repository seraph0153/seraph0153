import matplotlib.pyplot as plt
import matplotlib.animation as animation
import numpy as np

# Create a figure and axis
fig, ax = plt.subplots(figsize=(8, 6))

# Set up the scale representation
world_weight = 50
god_weight = 50
balance_point = 0

# Function to update the frame
def update(frame):
    ax.clear()
    ax.set_xlim(-100, 100)
    ax.set_ylim(-20, 20)
    ax.axis('off')

    # Update the weights
    global world_weight, god_weight, balance_point
    god_weight += 1
    balance_point = (god_weight - world_weight) / 2

    # Draw the scale
    ax.plot([balance_point, balance_point], [10, -10], color='black', lw=5)
    ax.plot([-100, 100], [0, 0], color='black', lw=3)
    ax.scatter(balance_point, 0, color='black', s=100)
    ax.text(-90, 2, "World", fontsize=15, color='red')
    ax.text(70, 2, "God", fontsize=15, color='green')

    # Draw the weights
    ax.plot([-50, balance_point], [0, 0], color='red', lw=5)
    ax.plot([balance_point, 50], [0, 0], color='green', lw=5)
    ax.scatter(-50, 0, color='red', s=300, label='World')
    ax.scatter(50, 0, color='green', s=300, label='God')

# Create the animation
ani = animation.FuncAnimation(fig, update, frames=np.arange(0, 50), repeat=False)

# Save the animation as an mp4 file
output_file = "scale_tipping_toward_god.mp4"
ani.save(output_file, writer='ffmpeg', fps=10)

plt.close()

print(f"Video saved as {output_file}")
