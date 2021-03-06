 
 
 # Ход работы
В качестве задания исходной матрицы, матрицы Фробениуса, вспомогательной матрицы S использовался собственный класс Matrix, в котором уже определены необходимые операции. Для превращения исходной матрицы в полином использовался класс Polynomial, который позволяет преобразовать полином в строчный вид для дальнейших вычислений. Элементами класса Polynom выступают экземпляры класса Fraction, который имеет метод toFraction(), позволяя представлять в качестве элементов полинома не только целые числа, но и вещественные, преобразованный в дробный вид, так как предоставленная библиотека PolStr умеет находить польскую строку только для выражений с целочисленными элементами.
В качестве метода для определения значения определителя матрицы был взят метод из предыдущей лабораторной работы, а именно метод Гаусса. 
Данные считываются из файла. Далее, в зависимости от выбранного типа задачи (задаётся в файле), программа высчитывает собственные числа или соответствующие собственные вектора.  И в том, и в другом случае выполняется подсчёт собственных чисел.

Для подсчёта собственных чисел получаем матрицу Фробениуса. Таким образом: 

- сначала инициализируем пока не построенную матрицу Фробениуса исходной матрицей;
- запоминаем промежуточную исходную матрицу, состояние которой понадобится при вычислении матрицы Фробениуса;
- инициализируем промежуточные матрицы M и M-1;
- инициализируем вспомогательную единичную матрицу.

Запускаем цикл, в котором:

- сначала получаем матрицу M, 
- перемножаем матрицу M справа на матрицу Фробениуса, результат записываем в матрицу Фробениуса, 
- а также перемножаем матрицу M с матрицей S, которая понадобится при вычислении собственных чисел, 
- вычисляем матрицу M-1;
- и наконец, домножаем только что полученную матрицу M-1 слева на матрицу Фробениуса, записываем результат произведения в матрицу Фробениуса.

Вычисленная матрица Фробениуса нужна для получения собственных чисел методом Данилевского. 
Инициализируем полином, коэффициенты которого составлены из нулевой строки матрицы Фробениуса. Далее следует вычислить корни полинома. Это реализовано простым перебором корней с шагом eps в промежутке, заданном в программе препроцессорными константами со значениями -10 и 10 соответственно. Значение считается корнем, если оно входит в допустимый промежуток по оси ординат, заданный также \delta\in[-eps,eps].
Если некоторый корень удовлетворяет всем условиям, то это ещё не значит, что он является фактическим корнем, т.к., как показано на рис. 2.2.2., нужно удостоверится, не будут ли последующие корни ближе к оси абсцисс, чем текущая. В программе реализован такой подход, что, если последующий корень ближе по модулю к оси абсцисс, чем предыдущий, то на текущем промежутке (удовлетворяющем условиям погрешности), следует считать его корнем. Корень установится, как только последующий корень по модулю будет больше предыдущего, боже если он всё ещё входит в промежуток заданной погрешности.
После вычисления текущего корня нужно проверить его кратность. Для этого вычислим производную функции в данном корне несколько раз, до тех пор, пока производная не станет равной нулю. Количество раз, которое мы вычислим производную, не встретив нулевую, и будет считаться кратностью корня.  При этом стоит заметить, что каждая последующая вычисленная производная в этой точке считается нулевой по несколько большему промежутку по оси ординат, по причине увеличивающейся погрешности вычислений в ЭВМ. В ходе экспериментов было выяснено, что коэффициентом корректировки можно считать значение 10. 
Вычисление собственных векторов исходит из значений собственных чисел непосредственно. Причём между собственными векторами матрицы Фробениуса и собственными векторами исходной матрицы существует прямая связь. Найдя собственные вектор по простой формуле 2.12, получаем собственный вектор исходной матрицы, умножив вычисленную на этапе получения матрицы Фробениуса матрицу M на текущий собственный вектор матрицы Фробениуса.
