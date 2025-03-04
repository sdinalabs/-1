# Словарь для преобразования цифр в прописной формат
digit_to_word = {
    '0': 'ноль',
    '1': 'один',
    '2': 'два',
    '3': 'три',
    '4': 'четыре',
    '5': 'пять',
    '6': 'шесть',
    '7': 'семь'
}

def is_octal_even(number):
    """Проверка, является ли число восьмеричным и четным."""
    try:
        return int(number, 8) % 2 == 0
    except ValueError:
        return False

def starts_with_odd_digit(number):
    """Проверка, начинается ли число с нечетной цифры."""
    return number[0] in {'1', '3', '5', '7'}

def process_number(number):
    """Обработка числа: нахождение минимальной и максимальной цифры и вывод их прописью."""
    min_digit = min(number)
    max_digit = max(number)
    return f"Минимальная цифра: {digit_to_word[min_digit]}, Максимальная цифра: {digit_to_word[max_digit]}"

def main(file_path, block_size=1024):
    """Основная функция для чтения файла и обработки лексем."""
    with open(file_path, 'r') as file:
        buffer = ""
        while True:
            block = file.read(block_size)
            if not block:
                break
            buffer += block
            while ' ' in buffer:
                space_pos = buffer.find(' ')
                lexeme = buffer[:space_pos]
                buffer = buffer[space_pos+1:]
                
                if len(lexeme) > 3 and lexeme.isdigit() and starts_with_odd_digit(lexeme) and is_octal_even(lexeme):
                    print(f"Число: {lexeme}")
                    print(process_number(lexeme))
                    print()

if __name__ == "__main__":
    file_path = "input.txt"  # Укажите путь к файлу
    main(file_path)
