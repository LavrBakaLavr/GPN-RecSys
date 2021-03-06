# GPN-RecSys
Рекомендательная система, выполненная в рамках GPN Intelligence Cup – направление Data Science

## Описание модели
В рамках проекта была разработана модель для рекомендации товаров на основе данных о покупках. В данной системе используется кластеризация товаров по группам и выдача рекомендаций на основе частоты покупок товаров разных групп вместе.

Кластеризация выполняется на основе названия товаров. Предполагается, что товары со схожим названием, скорее всего, принадлежат группе взаимозаменяемых товаров. В качестве векторайзера для текста используется TfidfVectorizer из библиотеки sklearn с двумя n-граммами. Так названия векторизуются как словосочетания, что должно дать хороший результат. Так как названия товаров не длинные, использовать длинные n-граммы нет смысла. В качестве модели для кластеризации используется алгоритм K ближайших соседей с ограничением по количеству выходных кластеров.

Рекомендации выдаются на основе частоты покупок товаров из разных кластеров вместе. Предполагается, что если товары из разных кластеров часто покупаются вместе, то такие товары являются взаимнодополняемыми. 

Результат по рекомендациям выводится в отдельный файл. 

Можно заметить, что модель выполнена несколько грубовато: алгоритм не оптимизирован, для выполнения программы до обработки файла transactions-for_submission уходит около часа в Google Collab, для обработки файла transactions-for_submission  требуется более 8 часов; при кластеризации не учитываются особенности товаров, кроме их названия; при составлении корреляционной матрицы не учитывается величина покупок; а самое главное, при составлении рекомендаций не учитываются предпочтения отдельных покупателей.

Предполагаемые доработки:
1)	Расширение корреляционной матрицы до трехмерной: в качестве дополнительных слоев выделить предпочтения отдельных покупателей по client_id. В качестве значений указать повышающий коэффициент. При выдаче рекомендаций учитывать корреляцию кластеров продуктов с учетом коэффициента предпочтений покупателя.
2)	При составлении корреляционной матрицы учитывать не только сам факт покупки товаров, но и другие данные, предоставленные в файле transactions.
3)	При векторизации товаров учитывать не только их название, но и другие особенности, предоставленные в файле nomenclature.
4)	Подобрать гиперпараметры для кластеризации. Протестировать другие алгоритмы кластеризации.
5)	Оптимизация функций составления корреляционной матрицы и функции рекомендаций для более быстрой обработки.
