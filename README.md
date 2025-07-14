# RETO 11 - STRINGS
1. Consulte que hacen los siguientes métodos de strings en python: endswith, startswith, isalpha, isalnum, isdigit, isspace, istitle, islower, isupper.
   
   * **endswith:** Devuelve ```True``` si la cadena termina con el sufijo (```suffix```) dado, de lo contrario, devuelve ```False```.
     
     ```python
     "archivo.txt".endswith(".txt")  # True
     ```
   * **startswith:** Devuelve ```True``` si la cadena comienza con el prefijo (```prefix```) dado, de lo contrario, ```False```.

     ```python
     "https://ejemplo.com".startswith("https")  # True
     ```
   * **isalpha:** Devuelve ```True``` si todos los caracteres de la cadena son letras del alfabeto (y la cadena no está vacía).
     
     ```python
     "Hola".isalpha()  # True
     "Hola123".isalpha()  # False
     ```
   * **isalnum:** Devuelve ```True``` si todos los caracteres son alfanuméricos (letras o números), y la cadena no está vacía.

      ```python
     ""abc123".isalnum()  # True
     "abc 123".isalnum()  # False (espacio)
     ```
   * **isdigit:** Devuelve ```True``` si todos los caracteres son dígitos (0-9), y hay al menos un carácter.
  
      ```python
     "12345".isdigit()  # True
     "123a5".isdigit()  # False
     ```
   * **isspace:** Devuelve ```True``` si todos los caracteres son espacios en blanco (como ```' '```, ```\n```, ```\t```), y hay al menos un carácter.
  
     ```python
     "   ".isspace()  # True
     "\t\n".isspace()  # True
     " a ".isspace()  # False
     ```
   * **istitle:** Devuelve ```True``` si la cadena está en formato título, es decir, cada palabra comienza con mayúscula y las siguientes letras son minúsculas.
  
     ```python
     "Hola Mundo".istitle()  # True
     "Hola mundo".istitle()  # False
     ```
   * **islower:** Devuelve ```True``` si todos los caracteres del texto son minúsculas y hay al menos una letra.
  
     ```python
     "python".islower()  # True
     "Python".islower()  # False
     ```
   * **isupper:** Devuelve ```True``` si todos los caracteres del texto son mayúsculas y hay al menos una letra.

      ```python
     "HOLA".isupper()  # True
     "Hola".isupper()  # False
     ```
2. Procesar el <a href="https://www.py4e.com/code3/mbox.txt">archivo</a> y extraer:
   * Cantidad de vocales
   * Cantidad de consonantes
   * Listado de las 50 palabras que más se repiten

   **SOLUCION**
 ```python
# Importamos las librerías necesarias
import urllib.request  # Sirve para leer archivos directamente desde internet
from collections import Counter  # Sirve para contar cuántas veces se repite cada palabra
# PASO 1: Leer el archivo desde internet
# Guardamos la dirección del archivo de texto
url = 'https://www.py4e.com/code3/mbox.txt'
# Abrimos la dirección usando urllib y guardamos la respuesta
respuesta = urllib.request.urlopen(url)
# Leemos todo el contenido del archivo y lo pasamos de bytes a texto
texto_completo = respuesta.read().decode('utf-8')
# PASO 2: Contar vocales y consonantes
# Creamos dos contadores, uno para las vocales y otro para las consonantes
cantidad_vocales = 0
cantidad_consonantes = 0
# Recorremos cada carácter del texto completo
for letra in texto_completo:
    # Verificamos si el carácter es una letra del alfabeto
    if letra.isalpha():
        # Convertimos la letra a minúscula para facilitar la comparación
        letra = letra.lower()
        # Si la letra está en el grupo de vocales, sumamos 1 al contador de vocales
        if letra in 'aeiou':
            cantidad_vocales += 1
        else:
            # Si no es vocal, entonces es consonante
            cantidad_consonantes += 1
# PASO 3: Preparar el texto para contar palabras
# Convertimos todo el texto a minúsculas para que no distinga entre mayúsculas y minúsculas
texto_minusculas = texto_completo.lower()
# Reemplazamos signos de puntuación por espacios para que no afecten el conteo de palabras
# Por ejemplo, si no quitamos los puntos, "correo." y "correo" se contarían como diferentes
texto_minusculas = texto_minusculas.replace('.', ' ')
texto_minusculas = texto_minusculas.replace(',', ' ')
texto_minusculas = texto_minusculas.replace(':', ' ')
texto_minusculas = texto_minusculas.replace(';', ' ')
texto_minusculas = texto_minusculas.replace('!', ' ')
texto_minusculas = texto_minusculas.replace('?', ' ')
texto_minusculas = texto_minusculas.replace('"', ' ')
texto_minusculas = texto_minusculas.replace("'", ' ')
texto_minusculas = texto_minusculas.replace('(', ' ')
texto_minusculas = texto_minusculas.replace(')', ' ')
texto_minusculas = texto_minusculas.replace('[', ' ')
texto_minusculas = texto_minusculas.replace(']', ' ')
# PASO 4: Contar palabras más repetidas
# Dividimos el texto en palabras, separando por espacios
lista_de_palabras = texto_minusculas.split()
# Usamos Counter para contar cuántas veces aparece cada palabra
conteo_palabras = Counter(lista_de_palabras)
# Obtenemos las 50 palabras más repetidas
palabras_mas_repetidas = conteo_palabras.most_common(50)
# Mostrar los resultados
# Imprimimos la cantidad total de vocales encontradas en el texto
print("Cantidad de vocales:", cantidad_vocales)
# Imprimimos la cantidad total de consonantes encontradas en el texto
print("Cantidad de consonantes:", cantidad_consonantes)
# Imprimimos las 50 palabras más repetidas y cuántas veces aparece cada una
print("\nLas 50 palabras más repetidas son:")
for palabra, cantidad in palabras_mas_repetidas:
    print(palabra, ":", cantidad)
```

