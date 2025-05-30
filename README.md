# angry-protons

# Задача
Протон влетает в магнитное поле так как его “запустил” пользователь (может под углом
не только прямым). Необходимо рассчитать траекторию полета протона в поле.
Построить графики траектории, зависимости скорости от времени, зависимости
ускорения от времени.

## Дополнительные задания
- “запустить” протон так, чтобы он попал в определенную цель
- протон влетает в неоднородное магнитное поле

# Скриншоты
![alt text](screenshots/image.png)
![alt text](screenshots/image2.png)
![alt text](screenshots/image3.png)
![alt text](screenshots/image4.png)

# Теоритическое обоснование
1) Однородное магнитное поле B
    Пусть скорость частицы - $\vec{v}$, угол $\vec{v}$ по отношению к полю $\vec{B}$ - $\alpha$:

    <img src="screenshots/teor1.png" alt="Теоретическое обоснование 1" width="50%">

    Выберем систему координат так, что ось $x || \vec{B}$, вектор $\vec{v}$ лежит в плоскости xOz

    <img src="screenshots/teor2.png" alt="Теоретическое обоснование 2" width="50%">

    Для движения вдоль поля (вдоль x):
    $v_x = const = v cos \alpha$

    Для движения в плоскости yOz:

    $m\vec{a_ц} = q[\vec{v}\vec{B}] = q v_z B = q v B sin \alpha$

    <img src="screenshots/teor3.png" alt="Теоретическое обоснование 3" width="25%">

    Движение по окружности: $\frac{m v_z^2}{R} = q v_z B$

    $\frac{m v_z}{R} = qB => R = \frac{m v sin \alpha}{qB}$ (или можно аналогично посчитать по теореме Пифагора)

    $v_z = wR; w = \frac{v_z}{R} = \frac{qB}{m}$ - угловая частота вращения

    $T = \frac{2 \pi}{ w} = \frac{2 \pi m}{qB}$ - период вращения

    Движение частицы - это движение по спирали:

    1) по окружности в плоскости yOz
    2) поступательно движение вдоль Ox

    ![alt text](screenshots/teor4.png)

    Таким образом, получим уравнение траектории, координаты которой уже можно рассчитать в программе в цикле t:

    $z = R cos wt$

    $y = R sin wt$

    $z = v_xt = v cos \alpha t$

    Для произвольного направления вектора $\vec{B}$, используется матрица поворота:

    ![Rotation Matrix](https://latex.codecogs.com/png.latex?%5Cdpi%7B120%7D%20%5Cbg_white%20R%28%5Ctheta%2C%5Cphi%29%20%3D%20%5Cbegin%7Bpmatrix%7D%20%5Ccos%5Cphi%20%5Ccos%5Ctheta%20%26%20-%5Csin%5Cphi%20%26%20%5Ccos%5Cphi%20%5Csin%5Ctheta%20%5C%5C%20%5Csin%5Cphi%20%5Ccos%5Ctheta%20%26%20%5Ccos%5Cphi%20%26%20%5Csin%5Cphi%20%5Csin%5Ctheta%20%5C%5C%20-%5Csin%5Ctheta%20%26%200%20%26%20%5Ccos%5Ctheta%20%5Cend%7Bpmatrix%7D)

2) Неоднородное поле
    При моделировании используется линеаризованное поле:

    $\vec{B}(\vec{r}) = \vec{B}_0 + (\nabla\vec{B})\cdot\vec{r}$

    Для случая неоднородного поля добавим интегрирование при помощи метода Эйлера:

    ![Euler Method](https://latex.codecogs.com/png.latex?%5Cdpi%7B120%7D%20%5Cbg_white%20%5Cbegin%7Baligned%7D%5Cvec%7Ba%7D_n%20%26%3D%20%5Cfrac%7Bq%7D%7Bm%7D%28%5Cvec%7Bv%7D_n%20%5Ctimes%20%5Cvec%7BB%7D%28%5Cvec%7Br%7D_n%29%29%20%5C%5C%20%5Cvec%7Bv%7D_%7Bn%2B1%7D%20%26%3D%20%5Cvec%7Bv%7D_n%20%2B%20%5Cvec%7Ba%7D_n%20%5CDelta%20t%20%5C%5C%20%5Cvec%7Br%7D_%7Bn%2B1%7D%20%26%3D%20%5Cvec%7Br%7D_n%20%2B%20%5Cvec%7Bv%7D_n%20%5CDelta%20t%20%5Cend%7Baligned%7D)

    Где $\Delta t$ - шаг интегрирования

3) Проверка попадания в цель

    Цель задается сферой с центром $(x_t, y_t, z_t)$ и радиусом $R_t$. Попадание регистрируется при выполнении условия:

    $\sqrt{(x - x_t)^2 + (y - y_t)^2 + (z - z_t)^2} \leq R_t$ для любой точки траектории
