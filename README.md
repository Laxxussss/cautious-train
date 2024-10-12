
import pygame
from pygame.locals import *
from OpenGL.GL import *
from OpenGL.GLU import *

# Define the vertices of a cube
vertices = [
    (1, -1, -1),
    (1, 1, -1),
    (-1, 1, -1),
    (-1, -1, -1),
    (1, -1, 1),
    (1, 1, 1),
    (-1, -1, 1),
    (-1, 1, 1)
]

# Define the edges connecting the vertices
edges = [
    (0, 1),
    (1, 2),
    (2, 3),
    (3, 0),
    (4, 5),
    (5, 6),
    (6, 7),
    (7, 4),
    (0, 4),
    (1, 5),
    (2, 6),
    (3, 7)
]

# Function to draw the cube
def draw_cube():
    glBegin(GL_LINES)  # Begin drawing lines
    for edge in edges:
        for vertex in edge:
            glVertex3fv(vertices[vertex])  # Draw each vertex
    glEnd()  # End drawing

# Main function to set up the environment and run the program
def main():
    # Initialize pygame
    pygame.init()
    display = (800, 600)  # Set display dimensions
    pygame.display.set_mode(display, DOUBLEBUF | OPENGL)  # Create display window
    pygame.display.set_caption("03 Lab 1 - Justin Padilla")  # Set window title

    # Set up perspective
    gluPerspective(45, (display[0] / display[1]), 0.1, 50.0)

    # Move viewer back by 5 units
    glTranslatef(0.0, 0.0, -5)

    # Main loop to keep the window running
    running = True
    while running:
        # Handle events (e.g., window close)
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

        # Clear the screen and depth buffer
        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)

        # Draw the cube
        draw_cube()

        # Update the display
        pygame.display.flip()

        # Pause for 10 milliseconds
        pygame.time.wait(10)

    # Quit pygame after the loop ends
    pygame.quit()

# Call the main function
if __name__ == "__main__":
    main()
