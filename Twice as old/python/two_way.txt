def twice_as_old(dad_years_old, son_years_old):
    count = 0
    if son_years_old == 0:
        return dad_years_old
    elif dad_years_old / son_years_old > 2:
        while son_years_old * 2 != dad_years_old:
            dad_years_old += 1
            son_years_old += 1
            count += 1
        return count
    elif dad_years_old / son_years_old < 2:
        while son_years_old != 0 and son_years_old * 2 != dad_years_old:
            dad_years_old -= 1
            son_years_old -= 1
            count += 1
        return count
    else:
        return 0