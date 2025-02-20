# Practicas
ejercicio 1

    import numpy as np
    def calculate(lst):
        if len(lst) != 9:
            raise ValueError("La lista debe contener nueve números")
        matrix = np.array(lst).reshape(3, 3)
        calculations = {
            'mean': [matrix.mean(axis=0).tolist(), matrix.mean(axis=1).tolist(), matrix.mean().tolist()],
            'variance': [matrix.var(axis=0).tolist(), matrix.var(axis=1).tolist(), matrix.var().tolist()],
            'standard deviation': [matrix.std(axis=0).tolist(), matrix.std(axis=1).tolist(), matrix.std().tolist()],
            'max': [matrix.max(axis=0).tolist(), matrix.max(axis=1).tolist(), matrix.max().tolist()],
            'min': [matrix.min(axis=0).tolist(), matrix.min(axis=1).tolist(), matrix.min().tolist()],
            'sum': [matrix.sum(axis=0).tolist(), matrix.sum(axis=1).tolist(), matrix.sum().tolist()]
        }

    return calculations
ejercicio 2

    import pandas as pd

    def load_data(file_path):
        """Carga los datos del archivo CSV."""
        return pd.read_csv(file_path)

    def demographic_analysis(df):
        """Realiza un análisis demográfico sobre el conjunto de datos."""
        total_entries = df.shape[0]
        race_count = df['race'].value_counts()
        avg_age_men = df[df['sex'] == 'Male']['age'].mean()
    
        higher_education = df[df['education'].isin(['Bachelors', 'Masters', 'Doctorate'])]
        higher_education_percentage = (higher_education.shape[0] / total_entries) * 100
        higher_education_rich = (higher_education[higher_education['salary'] == '>50K'].shape[0] / higher_education.shape[0]) * 100

        lower_education = df[~df['education'].isin(['Bachelors', 'Masters', 'Doctorate'])]
        lower_education_rich = (lower_education[lower_education['salary'] == '>50K'].shape[0] / lower_education.shape[0]) * 100
    

        min_work_hours = df['hours-per-week'].min()
    

        min_workers = df[df['hours-per-week'] == min_work_hours]
        rich_min_workers = (min_workers[min_workers['salary'] == '>50K'].shape[0] / min_workers.shape[0]) * 100
    

        country_salary_ratio = (df[df['salary'] == '>50K']['native-country'].value_counts() / df['native-country'].value_counts()) * 100
        highest_earning_country = country_salary_ratio.idxmax()
        highest_earning_country_percentage = country_salary_ratio.max()
    

        top_IN_occupation = df[(df['native-country'] == 'India') & (df['salary'] == '>50K')]['occupation'].value_counts().idxmax()
    
    return {
        'race_count': race_count,
        'avg_age_men': avg_age_men,
        'higher_education_percentage': higher_education_percentage,
        'higher_education_rich': higher_education_rich,
        'lower_education_rich': lower_education_rich,
        'min_work_hours': min_work_hours,
        'rich_min_workers': rich_min_workers,
        'highest_earning_country': highest_earning_country,
        'highest_earning_country_percentage': highest_earning_country_percentage,
        'top_IN_occupation': top_IN_occupation
    }

    def main():
        """Función principal para ejecutar el análisis."""
        file_path = 'adult.data.csv'  
        df = load_data(file_path)
        results = demographic_analysis(df)
        for key, value in results.items():
            print(f"{key}: {value}")

    if __name__ == "__main__":
        main()
