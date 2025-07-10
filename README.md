# Burger.py
Bouncing burger
import tkinter as tk
from PIL import Image, ImageTk
import random

class BouncingBurgerApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Bouncing Burger")

        # Canvas setup
        self.canvas_width = 800
        self.canvas_height = 600
        self.canvas = tk.Canvas(root, width=self.canvas_width, height=self.canvas_height, bg="white")
        self.canvas.pack()

        # Load transparent PNG image
        burger_img = Image.open("burger.png").resize((100, 100), Image.Resampling.LANCZOS)
        self.burger_photo = ImageTk.PhotoImage(burger_img)

        # Add image to canvas
        self.burger = self.canvas.create_image(100, 100, image=self.burger_photo, anchor=tk.NW)

        # Movement variables
        self.dx = 5
        self.dy = 4
        self.paused = False

        # Bind spacebar to pause/resume
        self.root.bind("<space>", self.toggle_pause)

        # Start animation loop
        self.animate()

    def toggle_pause(self, event=None):
        self.paused = not self.paused

    def animate(self):
        if not self.paused:
            self.move_burger()
        self.root.after(16, self.animate)

    def move_burger(self):
        x0, y0, x1, y1 = self.canvas.bbox(self.burger)
        hit_wall = False

        if x0 <= 0 or x1 >= self.canvas_width:
            self.dx = -self.dx
            hit_wall = True
        if y0 <= 0 or y1 >= self.canvas_height:
            self.dy = -self.dy
            hit_wall = True

        self.canvas.move(self.burger, self.dx, self.dy)

        if hit_wall:
            self.canvas.config(bg=self.random_color())

    def random_color(self):
        return "#{:06x}".format(random.randint(0, 0xFFFFFF))

# Run app
if __Nelson D. Pahayahay__ == "__main__":
    root = tk.Tk()
    app = BouncingBurgerApp(root)
    root.mainloop()
