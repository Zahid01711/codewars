import re
from operator import mul, truediv as div, add, sub


OPS = {'*': mul, '/': div, '-': sub, '+': add}


def calc(expression):
    tokens  = re.findall(r'[.\d]+|[()+*/-]', expression)
    return parse_AddSub(tokens, 0)[0]


def parse_AddSub(tokens, iTok):
    
    v, iTok = parse_MulDiv(tokens, iTok)
    
    while iTok < len(tokens) and tokens[iTok] != ')':
        tok   = tokens[iTok]
        if tok in '-+': 
            v2, iTok = parse_MulDiv(tokens, iTok+1)
            v = OPS[tok](v, v2)
    
    return v, iTok
    

def parse_MulDiv(tokens, iTok):
    
    v, iTok = parse_Term(tokens, iTok)
    
    while iTok < len(tokens) and tokens[iTok] in '*/': 
        op = tokens[iTok]
        v2, iTok = parse_Term(tokens, iTok+1)
        v = OPS[op](v, v2)
    
    return v, iTok


def parse_Term(tokens, iTok):
    tok = tokens[iTok]
    
    if tok == '(':
        v, iTok = parse_AddSub(tokens, iTok+1)
        if iTok < len(tokens) and tokens[iTok] != ')': raise Exception()
        
    elif tok == '-':
        v, iTok = parse_Term(tokens, iTok+1)
        v, iTok = -v, iTok-1
        
    else:
        v = float(tok)
    
    return v, iTok+1