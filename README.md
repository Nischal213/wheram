from prettytable import PrettyTable


def create_table(
    first_row, constant_abs_uncertain=False, avg_data=False, square_wanted=False, dp=int
):
    table = PrettyTable()
    table.field_names = [
        first_row,
        f"{first_row} absolute uncertainty",
        f"{first_row} relative uncertainty",
    ]
    rows = []
    if avg_data:
        if square_wanted:
            table = PrettyTable()
            table.field_names = [
                first_row,
                f"{first_row} absolute uncertainty",
                f"{first_row} relative(%) uncertainty",
                f"{first_row} squared",
                f"{first_row} squared absolute uncertainty",
                f"{first_row} squared relative(%) uncertainty",
            ]
            repeat = int(input("How many repeats? "))
            for i in range(1, 7):
                avg_value = 0
                temp_lst = []
                print(f"{i}th row")
                for j in range(1, repeat + 1):
                    value = float(input(f"Enter the {j}th value: "))
                    temp_lst.append(value)
                for h in temp_lst:
                    avg_value += h
                abs_uncertain = round((max(temp_lst) - min(temp_lst)) / 2, dp)
                avg_value = round(avg_value / repeat, dp)
                rel_uncertain = round((abs_uncertain / avg_value) * 100, dp)
                rel_uncertain_squared = round(rel_uncertain**2, dp)
                abs_uncertain_squared = round(
                    (avg_value**2) * (rel_uncertain_squared / 100), dp
                )
                avg_value_squared = round(avg_value**2, dp)
                rows.append(
                    [
                        avg_value,
                        abs_uncertain,
                        rel_uncertain,
                        avg_value_squared,
                        abs_uncertain_squared,
                        rel_uncertain_squared,
                    ]
                )
        else:
            repeat = int(input("How many repeats? "))
            for i in range(1, 7):
                avg_value = 0
                temp_lst = []
                print(f"{i}th row")
                for j in range(1, repeat + 1):
                    value = float(input(f"Enter the {j}th value: "))
                    temp_lst.append(value)
                for h in temp_lst:
                    avg_value += h
                abs_uncertain = round((max(temp_lst) - min(temp_lst)) / 2, dp)
                avg_value = round(avg_value / repeat, dp)
                rel_uncertain = round((abs_uncertain / avg_value) * 100, dp)
                rows.append([avg_value, abs_uncertain, rel_uncertain])
    else:
        if constant_abs_uncertain:
            if square_wanted:
                table = PrettyTable()
                table.field_names = [
                    first_row,
                    f"{first_row} absolute uncertainty",
                    f"{first_row} relative uncertainty",
                    f"{first_row} squared absolute uncertainty",
                    f"{first_row} squared relative uncertainty",
                ]
                abs_uncertain = float(input(f"Enter the absolute uncertainty: "))
                for i in range(1, 7):
                    value = float(input(f"Enter {i}th value: "))
                    rel_uncertain = round((abs_uncertain / value) * 100, dp)
                    rel_uncertain_squared = round(rel_uncertain**2, dp)
                    abs_uncertain_squared = round(
                        (value**2) * rel_uncertain_squared, dp
                    )
                    rows.append(
                        [
                            value,
                            abs_uncertain,
                            rel_uncertain,
                            abs_uncertain_squared,
                            rel_uncertain_squared,
                        ]
                    )
            else:
                abs_uncertain = float(input(f"Enter the absolute uncertainty: "))
                for i in range(1, 7):
                    value = float(input(f"Enter {i}th value: "))
                    rel_uncertain = round((abs_uncertain / value) * 100, dp)
                    rows.append([value, abs_uncertain, rel_uncertain])
        else:
            if square_wanted:
                table = PrettyTable()
                table.field_names = [
                    first_row,
                    f"{first_row} absolute uncertainty",
                    f"{first_row} relative uncertainty",
                    f"{first_row} squared absolute uncertainty",
                    f"{first_row} squared relative uncertainty",
                ]
                for i in range(1, 7):
                    value = float(input(f"Enter {i}th value: "))
                    abs_uncertain = float(input(f"Enter the absolute uncertainty: "))
                    rel_uncertain = round((abs_uncertain / value) * 100, dp)
                    rel_uncertain_squared = round(rel_uncertain**2, dp)
                    abs_uncertain_squared = round(
                        (value**2) * rel_uncertain_squared, dp
                    )
                    rows.append(
                        [
                            value,
                            abs_uncertain,
                            rel_uncertain,
                            abs_uncertain_squared,
                            rel_uncertain_squared,
                        ]
                    )
            else:
                for i in range(1, 7):
                    value = float(input(f"Enter {i}th value: "))
                    abs_uncertain = float(input(f"Enter the absolute uncertainty: "))
                    rel_uncertain = round((abs_uncertain / value) * 100, dp)
                    rows.append([value, abs_uncertain, rel_uncertain])
    for i in rows:
        table.add_row(i)
    print(
        f"* Bear in mind that float() in python will remove 0 so just add it back when copying *\n* Decimal places used: {dp} dp *\n{table}"
    )


constant_uncertain = input("Does it have a constant uncertainty? (y/n) ").lower()
if constant_uncertain in ["n", "no"]:
    constant_uncertain = False
data_type = input("Is it an average data? (y/n) ")
if data_type in ["n", "no"]:
    data_type = False
square_wanted = input("Do you also want the squared variants? (y/n): ")
if square_wanted in ["n", "no"]:
    square_wanted = False
dp = int(input("To how many d.p? "))
variable_name = input("Enter variable name: ")
create_table(variable_name, constant_uncertain, data_type, square_wanted, dp)
