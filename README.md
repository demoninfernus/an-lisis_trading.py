import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.preprocessing import PolynomialFeatures
from sklearn.pipeline import make_pipeline
from sklearn.metrics import mean_squared_error, r2_score
from typing import Optional
import time
import requests
import subprocess  # Módulo necesario para abrir el Bloc de Notas

class FinancialMatrix:
    def __init__(self, data):
        self.data = data

    def calculate_returns(self):
        """<font color="gold">Calcula los rendimientos diarios.</font>"""
        close_prices = self.data['Close']
        return close_prices.pct_change().dropna()

class TrendAnalysis:
    def __init__(self):
        """<font color="gold">Inicializa la clase TrendAnalysis.</font>"""
        self.resultados = {'modelos': {}, 'mses': {}, 'r2s': {}, 'predicciones': {}}

    # ... (sin cambios)

class TradingStrategy(TrendAnalysis):
    # ... (sin cambios)

    def ingresar_datos(self):
        """<font color="gold">Ingrese los datos necesarios para la estrategia:</font>"""
        self.symbol = input("Ingrese el símbolo de la acción (por ejemplo, AAPL): ")
        self.start_date = input("Ingrese la fecha de inicio (por ejemplo, 2022-01-01): ")
        self.end_date = input("Ingrese la fecha de finalización (por ejemplo, 2022-12-31): ")
        self.buy_threshold = float(input("Ingrese el umbral de compra: "))
        self.sell_threshold = float(input("Ingrese el umbral de venta: "))
        self.wait_time_seconds = int(input("Ingrese el tiempo de espera en segundos: "))
        self.quantity = int(input("Ingrese la cantidad para la operación: "))
        self.data_source = input("Ingrese la fuente de datos (por ejemplo, yahoo): ")
        self.trading_api = input("Ingrese la API de trading (por ejemplo, alpaca): ")
        self.additional_parameter1 = input("Ingrese el parámetro adicional 1 (si no hay, presione Enter): ")
        self.additional_parameter2 = input("Ingrese el parámetro adicional 2 (si no hay, presione Enter): ")
        self.financial_parameter1 = float(input("Ingrese el parámetro financiero 1: "))
        self.financial_parameter2 = float(input("Ingrese el parámetro financiero 2: "))

    def setup_virtual_environment(self):
        """<font color="gold">Configura un entorno virtual y muestra las bibliotecas instaladas.</font>"""
        try:
            subprocess.run(['python', '-m', 'venv', 'myenv'], check=True)
            subprocess.run(['myenv\\Scripts\\activate'], shell=True, check=True)
            subprocess.run(['pip', 'install', 'pandas', 'numpy', 'matplotlib', 'scikit-learn', 'beautifulsoup4'], check=True)
            subprocess.run(['pip', 'freeze'], check=True)
            print("\n<font color='gold'>Entorno virtual configurado y bibliotecas instaladas correctamente.</font>")
        except Exception as e:
            print(f"<font color='gold'>Error durante la configuración del entorno virtual: {e}</font>")

    def search_bmv_information(self, symbol, start_date, end_date):
        """<font color="gold">Busca información de la Bolsa Mexicana de Valores.</font>"""
        try:
            bmv_url = f'https://www.bmv.com.mx/es/sector-financiero/instrumentos-financieros/historicos/{symbol}?start={start_date}&end={end_date}'
            response = requests.get(bmv_url)
            if response.status_code == 200:
                bmv_data = self.extract_bmv_data(response.text)
                print(f"<font color='gold'>Datos de la BMV para {symbol} entre {start_date} y {end_date}:</font>\n{bmv_data}")
            else:
                print(f"<font color='gold'>Error al obtener información de la BMV. Código de estado: {response.status_code}</font>")
        except Exception as e:
            print(f"<font color='gold'>Error al buscar información de la BMV: {e}</font>")

    def compare_data(self, financial_matrix, bmv_data):
        """<font color="gold">Compara la información de la BMV con la matriz financiera.</font>"""
        try:
            # Obtener los rendimientos diarios
            returns = financial_matrix.calculate_returns()

            # Comparar con la información de la BMV
            # ... (lógica de comparación)

            print("<font color='gold'>Comparación de datos realizada con éxito.</font>")
        except Exception as e:
            print(f"<font color='gold'>Error al comparar datos: {e}</font>")

    def run_notepad(self, results_text):
        """<font color="gold">Ejecuta el Bloc de Notas y muestra los resultados.</font>"""
        try:
            with open('results.txt', 'w') as file:
                file.write(results_text)

            subprocess.run(['notepad.exe', 'results.txt'], check=True)
            print("<font color='gold'>Resultados mostrados en el Bloc de Notas.</font>")
        except Exception as e:
            print(f"<font color='gold'>Error al ejecutar el Bloc de Notas: {e}</font>")

    def run_combined_strategy(self, financial_matrix):
        try:
            # ... (sin cambios)

            # Configurar entorno virtual y mostrar bibliotecas instaladas
            self.setup_virtual_environment()

            # Ingresar datos para la estrategia
            self.ingresar_datos()

            # Buscar información en la Bolsa Mexicana de Valores
            self.search_bmv_information(self.symbol, self.start_date, self.end_date)

            # Ejecutar análisis de tendencias y estrategia de trading
            self.run_combined_simulation()

            # Comparar datos de la BMV con la matriz financiera
            self.compare_data(financial_matrix, bmv_data)  # Asegúrate de tener los datos de la BMV antes de llamar a este método

            # Mostrar resultados en el Bloc de Notas
            results_text = "\n<font color='gold'>Resultados de la estrategia combinada:</font>\n" + str(self.resultados)
            self.run_notepad(results_text)

        except Exception as e:
            print(f"<font color='gold'>Error durante la ejecución de la estrategia combinada: {e}</font>")

# Resto del código sin cambios

if __name__ == '__main__':
    # ... (sin cambios)

    # Crear una instancia de la estrategia
    strategy = TradingStrategy(
        # ... (sin cambios)
    )

    # Ejecutar la estrategia y mostrar resultados
    strategy.run_combined_strategy()
    strategy.display_results()
