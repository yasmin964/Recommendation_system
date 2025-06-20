# User-Based Movie Recommender System 🎬

Этот проект реализует рекомендательную систему фильмов на основе **коллаборативной фильтрации по пользователям**, используя датасет [MovieLens 100K](https://grouplens.org/datasets/movielens/100k/).

## 📁 Структура проекта

- `u.data` — оценки фильмов пользователями (user_id, item_id, rating, timestamp)
- `u.item.csv` — метаданные фильмов (movie_id, title и др.)
- `recommender.ipynb` / `recommender.py` — основная реализация рекомендательной системы

## 🚀 Как работает

1. **Загрузка и предобработка данных**
   - Импортируются оценки пользователей.
   - Разделяются на тренировочную и тестовую выборки по каждому пользователю.

2. **Формирование матрицы "пользователь-фильм"**
   - Создается сводная таблица `user_item`, где строки — пользователи, столбцы — фильмы, значения — рейтинги.

3. **Подсчет схожести между пользователями**
   - Используется **косинусное сходство** для построения матрицы схожести.

4. **Генерация рекомендаций**
   - Для целевого пользователя находятся `k` наиболее похожих пользователей.
   - Их оценки агрегируются с учетом коэффициента схожести.
   - Исключаются фильмы, которые пользователь уже смотрел.
   - Выдаются `n` фильмов с наивысшими взвешенными оценками.

5. **Оценка качества**
   - Вычисляется **Precision@k** на тестовой выборке: насколько часто рекомендованные фильмы действительно встречаются в реальных оценках.

## 📊 Пример использования

```python
recommendations = recommend_movie(target_user=1, k=5, n_recommendations=5)
print("Recommended movie IDs:\n", recommendations)

# Получение названий фильмов
movie_titles = movie.set_index('movie id ')
print(movie_titles.loc[recommendations.index][' movie title '])
