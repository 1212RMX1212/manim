from manim import *
import numpy as np

class SuperficiesActividad1(ThreeDScene):
    def construct(self):
        axes = ThreeDAxes()
        
        elipsoide = Surface(
            lambda u, v: np.array([
                3 * np.sin(u) * np.cos(v),
                2 * np.sin(u) * np.sin(v),
                3 * np.cos(u)
            ]), u_range=[0, PI], v_range=[0, 2*PI],
            checkerboard_colors=[BLUE_D, BLUE_E], resolution=(20, 40)
        )
        self.set_camera_orientation(phi=75 * DEGREES, theta=-45 * DEGREES)
        self.add(axes)
        
        
        self.play(Create(elipsoide))
        self.wait(2)
        self.play(FadeOut(elipsoide))
        self.begin_ambient_camera_rotation(rate=0.2)
        self.wait(3)
