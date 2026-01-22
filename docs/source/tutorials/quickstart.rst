from manim import *
import numpy as np

class SuperficiesActividad1(ThreeDScene):
    def construct(self):
        axes = ThreeDAxes()
        
        # a) Elipsoide: x²/9 + y²/4 + z²/9 = 1
        # Parametrización: x = 3sin(u)cos(v), y = 2sin(u)sin(v), z = 3cos(u)
        elipsoide = Surface(
            lambda u, v: np.array([
                3 * np.sin(u) * np.cos(v),
                2 * np.sin(u) * np.sin(v),
                3 * np.cos(u)
            ]), u_range=[0, PI], v_range=[0, 2*PI],
            checkerboard_colors=[BLUE_D, BLUE_E], resolution=(20, 40)
        )

        # b) Hiperboloide de dos hojas: z² - x² - y² = 1
        # Parte superior (z >= 1): z = sqrt(1 + x² + y²)
        hiperboloide = Surface(
            lambda u, v: np.array([
                np.sinh(u) * np.cos(v),
                np.sinh(u) * np.sin(v),
                np.cosh(u)
            ]), u_range=[0, 1.5], v_range=[0, 2*PI],
            checkerboard_colors=[RED_D, RED_E]
        )
        # Parte inferior (z <= -1)
        hiperboloide_inf = hiperboloide.copy().scale([1, 1, -1])

        # c) Cono: x² + y² = z² -> z = sqrt(x² + y²)
        cono = Surface(
            lambda u, v: np.array([
                u * np.cos(v),
                u * np.sin(v),
                u
            ]), u_range=[-2, 2], v_range=[0, 2*PI],
            checkerboard_colors=[GREEN_D, GREEN_E]
        )

        # Animación
        self.set_camera_orientation(phi=75 * DEGREES, theta=-45 * DEGREES)
        self.add(axes)
        
        # Mostrar Elipsoide
        self.play(Create(elipsoide))
        self.wait(2)
        self.play(FadeOut(elipsoide))

        # Mostrar Hiperboloide
        self.play(Create(hiperboloide), Create(hiperboloide_inf))
        self.wait(2)
        self.play(FadeOut(hiperboloide), FadeOut(hiperboloide_inf))

        # Mostrar Cono
        self.play(Create(cono))
        self.begin_ambient_camera_rotation(rate=0.2)
        self.wait(3)
