### PASOS PARA UTILIZAR STREAMLIT

1. Instalar Streamlit: 
```python
!pip install -q streamlit 
````
2. Devuelve una URL
```python 
get_ipython().system_raw('./ngrok http 8501 &') 
! curl -s http://localhost:4040/api/tunnels | python3 -c \
"import sys, json; print(json.load(sys.stdin)['tunnels'][0]['public_url'])"
```
3. Importa streamlit y creas el ficheo .py
```python
%%file test.py 
import streamlit as st
st.title("Pagina test")
st.markdown("""# Hemos registrado la esperanza de vida y la renta per capita en varios países
* Opcion 1
* Opcion 2
* Opcion 3

*negrita*"""

st.write(chart_life) #*altair*
st.bokeh_chart(nombre) #*bokeh*
```
4. Ejecuto el fichero test.py. Solo ficheros .py
```python
!streamlit run test.py
```
