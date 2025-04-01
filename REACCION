import streamlit as st
from sympy import symbols, Eq, solve

def balance_combustion(formula):
    # Identificar átomos en el hidrocarburo
    import re
    match = re.match(r'C(\d*)H(\d*)', formula)
    if not match:
        return "Fórmula inválida. Usa el formato CxHy, por ejemplo, C3H8."
    
    C = int(match.group(1)) if match.group(1) else 1
    H = int(match.group(2)) if match.group(2) else 1
    
    # Definir variables
    a, b, c, d = symbols('a b c d')
    eq1 = Eq(a, c)
    eq2 = Eq(2 * a, d)
    eq3 = Eq(b, 2 * c + d / 2)
    
    # Resolver sistema de ecuaciones
    sol = solve((eq1, eq2, eq3), (a, b, c, d))
    a_val, b_val, c_val, d_val = sol[a] * C, sol[b] * C, sol[c] * C, sol[d] * C
    
    return f"{a_val} C{C}H{H} + {b_val} O2 → {c_val} CO2 + {d_val} H2O"

# Interfaz en Streamlit
st.title("Balanceador de Reacciones de Combustión")
hydrocarbon = st.text_input("Introduce la fórmula del hidrocarburo (Ejemplo: C3H8)")
if hydrocarbon:
    balanced_equation = balance_combustion(hydrocarbon)
    st.write("Reacción balanceada:")
    st.latex(balanced_equation)
