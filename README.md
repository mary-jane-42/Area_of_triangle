# Area_of_triangle
import streamlit as st
import numpy as np

st.title("🔺 General Triangle Area Calculator")

triangle_type = st.selectbox(
    "Select the method to calculate area:",
    [
        "By Base and Height",
        "By Three Sides (Heron's Formula)",
        "By Two Sides and Included Angle"
    ]
)

def area_base_height(base, height):
    return 0.5 * base * height

def area_heron(a, b, c):
    s = (a + b + c) / 2
    try:
        area = np.sqrt(s * (s - a) * (s - b) * (s - c))
        return area
    except:
        return None

def area_two_sides_angle(a, b, angle_deg):
    angle_rad = np.radians(angle_deg)
    return 0.5 * a * b * np.sin(angle_rad)

st.markdown("---")

if triangle_type == "By Base and Height":
    base = st.number_input("Enter base (units):", min_value=0.0)
    height = st.number_input("Enter height (units):", min_value=0.0)
    if st.button("Calculate Area"):
        area = area_base_height(base, height)
        st.success(f"Area: {area:.2f} square units")

elif triangle_type == "By Three Sides (Heron's Formula)":
    a = st.number_input("Enter side a (units):", min_value=0.0)
    b = st.number_input("Enter side b (units):", min_value=0.0)
    c = st.number_input("Enter side c (units):", min_value=0.0)
    if st.button("Calculate Area"):
        if a + b > c and a + c > b and b + c > a:
            area = area_heron(a, b, c)
            st.success(f"Area: {area:.2f} square units")
        else:
            st.error("Invalid triangle sides — they must satisfy the triangle inequality.")

elif triangle_type == "By Two Sides and Included Angle":
    a = st.number_input("Enter side a (units):", min_value=0.0)
    b = st.number_input("Enter side b (units):", min_value=0.0)
    angle = st.number_input("Enter included angle (degrees):", min_value=0.0, max_value=180.0)
    if st.button("Calculate Area"):
        area = area_two_sides_angle(a, b, angle)
        st.success(f"Area: {area:.2f} square units")

