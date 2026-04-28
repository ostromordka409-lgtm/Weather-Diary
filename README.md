import json import tkinter as tk from tkinter import ttk, messagebox, filedialog from datetime import datetime

class WeatherDiary: def init(self, root): self.root = root self.root.title("Weather Diary") self.records = []

# Input fields
    frame = tk.Frame(root)
    frame.pack(pady=10)

    tk.Label(frame, text="Дата (YYYY-MM-DD)").grid(row=0, column=0)
    self.date_entry = tk.Entry(frame)
    self.date_entry.grid(row=0, column=1)

    tk.Label(frame, text="Температура (°C)").grid(row=1, column=0)
    self.temp_entry = tk.Entry(frame)
    self.temp_entry.grid(row=1, column=1)

    tk.Label(frame, text="Описание").grid(row=2, column=0)
    self.desc_entry = tk.Entry(frame)
    self.desc_entry.grid(row=2, column=1)

    self.rain_var = tk.BooleanVar()
    tk.Checkbutton(frame, text="Осадки", variable=self.rain_var).grid(row=3, columnspan=2)

    tk.Button(frame, text="Добавить запись", command=self.add_record).grid(row=4, columnspan=2, pady=5)

    # Filter
    filter_frame = tk.Frame(root)
    filter_frame.pack(pady=10)

    tk.Label(filter_frame, text="Фильтр по дате").grid(row=0, column=0)
    self.filter_date = tk.Entry(filter_frame)
    self.filter_date.grid(row=0, column=1)

    tk.Label(filter_frame, text="Температура >").grid(row=1, column=0)
    self.filter_temp = tk.Entry(filter_frame)
    self.filter_temp.grid(row=1, column=1)

    tk.Button(filter_frame, text="Применить фильтр", command=self.apply_filter).grid(row=2, columnspan=2)

    # Table
    self.tree = ttk.Treeview(root, columns=("date", "temp", "desc", "rain"), show='headings')
    for col in ("date", "temp", "desc", "rain"):
        self.tree.heading(col, text=col)
    self.tree.pack(pady=10)

    # Buttons for file
    btn_frame = tk.Frame(root)
    btn_frame.pack()

    tk.Button(btn_frame, text="Сохранить", command=self.save_json).grid(row=0, column=0)
    tk.Button(btn_frame, text="Загрузить", command=self.load_json).grid(row=0, column=1)

def validate(self, date, temp, desc):
    try:
        datetime.strptime(date, "%Y-%m-%d")
    except ValueError:
        messagebox.showerror("Ошибка", "Неверный формат даты")
        return False

    try:
        float(temp)
    except ValueError:
        messagebox.showerror("Ошибка", "Температура должна быть числом")
        return False

    if not desc.strip():
        messagebox.showerror("Ошибка", "Описание не должно быть пустым")
        return False

    return True

def add_record(self):
    date = self.date_entry.get()
    temp = self.temp_entry.get()
    desc = self.desc_entry.get()
    rain = self.rain_var.get()

    if not self.validate(date, temp, desc):
        return

    record = {
        "date": date,
        "temp": float(temp),
        "desc": desc,
        "rain": rain
    }
    self.records.append(record)
    self.update_table(self.records)

def update_table(self, data):
    for row in self.tree.get_children():
        self.tree.delete(row)
    for rec in data:
        self.tree.insert('', tk.END, values=(rec['date'], rec['temp
