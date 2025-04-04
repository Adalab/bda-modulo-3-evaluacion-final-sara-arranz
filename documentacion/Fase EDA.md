
# Conocimiento de los archivos

## Archivo: Customer Loyalty History, df_clientes

- Contiene información de los clientes que han hecho uso de la aerolínea

- Columnas de registro:'Loyalty Number', 'Country', 'Province', 'City', 'Postal Code',
    'Gender', 'Education', 'Salary', 'Marital Status', 'Loyalty Card',
    'CLV', 'Enrollment Type', 'Enrollment Year', 'Enrollment Month',
    'Cancellation Year', 'Cancellation Month'.
    
    Se modiican el nombre de las columnas generando _ en lso espacios entre palabras

- Tamaño del registro = 16.737 filas y 16 columnas orignales

- Revisión general:
       Column              Non-Null Count  Dtype  
---  ------              --------------  -----  
 0   Loyalty Number      16737 non-null  int64      Identificador único del cliente. No tiene datos nulos y su tipo de dato es correcto
 1   Country             16737 non-null  object     País de residencia. No tiene datos nulos y su tipo de dato es correcto
 2   Province            16737 non-null  object     Provincia de residencia. No tiene datos nulos y su tipo de dato es correcto
 3   City                16737 non-null  object     Ciudad de residencia. No tiene datos nulos y su tipo de dato es correcto
 4   Postal Code         16737 non-null  object     Código postal. No tiene datos nulos y su tipo de dato es correcto (ejemplo:M2Z 4K1)
 5   Gender              16737 non-null  object     Género. No tiene datos nulos y su tipo de dato es correcto
 6   Education           16737 non-null  object     Nivel educativo alcanzado.  No tiene datos nulos y su tipo de dato es correcto
 7   Salary              12499 non-null  float64    Salario. Tiene datos nulos, su tipo de dato NO es correcto (TODOS LOS VALORES SON INT)
 8   Marital Status      16737 non-null  object     Estado civil.  Tiene datos nulos, su tipo de dato es correcto
 9   Loyalty Card        16737 non-null  object     Tipo de tarjeta de lealtad. Tiene datos nulos, su tipo de dato es correcto (ejemplo: star)
 10  CLV                 16737 non-null  float64    Valor total estimado que el cliente aporta a la empresa. Tiene datos nulos, su tipo de dato es correcto
 11  Enrollment Type     16737 non-null  object     Tipo de inscripción del cliente en el programa de lealtad (ej. Standard). Tiene nulos y el tipo de dato correcto
 12  Enrollment Year     16737 non-null  int64      Año en que el cliente se inscribió. Tiene nulos. Vamos a unificar con la siguiente columna.
 13  Enrollment Month    16737 non-null  int64      Mes en que el cliente se inscribió. Tiene nulos. Unificamos con year y ponemos tipo dato para fecha sin registro día.
 14  Cancellation Year   2067 non-null   float64    Año en que el cliente canceló su suscripción.Tiene una gran cantidad de nulos. Tipo de dato NO es correcto(INT)
 15  Cancellation Month  2067 non-null   float64    Mes en que el cliente canceló su suscripción.Tiene una gran cantidad de nulos. Tipo de dato NO es correcto(INT)

- Resumen de transformaciones necesarias en cuanto al tipo de dato de la columna:
       - Salary float64, su tipo de dato NO es correcto (TODOS LOS VALORES SON INT)
       - Cancellation Year float64, su tipo de dato NO es correcto(INT)
       - Cancellation Month float64, su tipo de dato NO es correcto(INT)


- Registro sin duplicados.

- Porcetaje de valores nulos:

       Salary                25.321145
       Cancellation Year     87.650117
       Cancellation Month    87.650117

        Decisión y valoración: Se eliminan las columnas de Cancellation en el df_clientes dado el procentaje elevado de valores nulos. Se genera un dataset df_clientes_bajas con los datos de los clientes que sí han anulado su suscripción. Por si más adelnate fuera necesario trabajar con este tipo de clientes en concreto. EL DATA SET SE LLAMA df_clientes_bajas

        Se trabaja en la columna Salary a través de los datos estadísticos de la misma y se decide sustituir los valores nulos por el valor de la mediana de los salarios. La desviación relativa (en porcentaje) sería:

       Desviación relativa=(−1495.05/79,359.34)×100≈−1.88%

       Esto significa que la media después de la imputación con la mediana es aproximadamente un 1.88% más baja que la original. Dependiendo del contexto de tu análisis, este porcentaje podría no ser tan significativo. Teniendo en cuenta que el estudio se centra en los clientes y la productividad de una aerolínea, y que el salario es un dato secundario, manejo y corroboro esta imputación.


- Revisión de datos únicos en las columnas categóricas:

['Canada']
['Ontario' 'Alberta' 'British Columbia' 'Quebec' 'Yukon' 'New Brunswick'
 'Manitoba' 'Nova Scotia' 'Saskatchewan' 'Newfoundland'
 'Prince Edward Island']
['Toronto' 'Edmonton' 'Vancouver' 'Hull' 'Whitehorse' 'Trenton' 'Montreal'
 'Dawson Creek' 'Quebec City' 'Fredericton' 'Ottawa' 'Tremblant' 'Calgary'
 'Thunder Bay' 'Whistler' 'Peace River' 'Winnipeg' 'Sudbury'
 'West Vancouver' 'Halifax' 'London' 'Regina' 'Kelowna' "St. John's"
 'Victoria' 'Kingston' 'Banff' 'Moncton' 'Charlottetown']
['M2Z 4K1' 'T3G 6Y6' 'V6E 3D9' 'P1W 1K4' 'J8Y 3Z5' 'Y2K 6R0' 'P5S 6R4'
 'K8V 4B2' 'H2Y 2W2' 'M8Y 4K8' 'U5I 4F1' 'G1B 3L5' 'H4G 3T4' 'M2M 7K8'
 'M2M 6J7' 'E3B 2H2' 'M1R 4K3' 'T9G 1W3' 'H2Y 4R4' 'V5R 1W3' 'P1L 8X8'
 'K1F 2R2' 'H5Y 2S9' 'V1E 4R6' 'H2T 2J6' 'T3E 2V9' 'H2T 9K8' 'K8T 5M5'
 'V6T 1Y8' 'P2T 6G3' 'T9O 2W2' 'V6E 3Z3' 'R6Y 4T5' 'M5V 1G5' 'V6V 8Z3'
 'B3J 9S2' 'M5B 3E4' 'R2C 0M5' 'S6J 3G0' 'M2P 4F6' 'P1J 8T7' 'V09 2E9'
 'A1C 6H9' 'V10 6T5' 'B3C 2M8' 'M9K 2P4' 'T4V 1D4' 'R3R 3T4' 'S1J 3C5'
 'E1A 2A7' 'K1G 4Z0' 'H3T 8L4' 'C1A 6E8' 'H3J 5I6' 'M3R 4K8']
['Female' 'Male']
['Bachelor' 'College' 'Master' 'High School or Below' 'Doctor']
['Married' 'Divorced' 'Single']
['Star' 'Aurora' 'Nova']

       Al igual que en las columnas, se generan _ en los espacios entre palabras y nos aseguramos de eliminar espacios innecesarios al ppo y final de cada dato

Finalmente se elimina la columna country ya que todos los clientes son de Canadá y se añade el símbolo del $ dado que es la moneda de eso del país de registro de los clientes.

## Archivo: Customer Flight Analysis.csv, df_vuelos

- Revisión general:

RangeIndex: 405624 entries, 0 to 405623
Data columns (total 10 columns):
        Column                       Non-Null Count   Dtype  
---  ------                       --------------   -----  
 0   Loyalty_Number               405624 non-null  int64  
 1   Year                         405624 non-null  int64  
 2   Month                        405624 non-null  int64  
 3   Flights_Booked               405624 non-null  int64  
 4   Flights_with_Companions      405624 non-null  int64  
 5   Total_Flights                405624 non-null  int64  
 6   Distance                     405624 non-null  int64  
 7   Points_Accumulated           405624 non-null  float64
 8   Points_Redeemed              405624 non-null  int64  
 9   Dollar_Cost_Points_Redeemed  405624 non-null  int64  

- Tiene una columna en común con el df_clientes: Loyalty Number

- Tiene duplicados

Los estudio y no tengo seguridad en proceder a su eliminación debido a la gran variedad de datos que se recogen de un mismo cliente en fechas diversas.

- No tiene nulos

- Tipos de dato en columnas correcto, unificamos las columnas de year y month en la misma y cambiamos el tipo de dato al que corresponde.
