# Python-01
# -*- coding:Utf-8 -*-
from numpy import *
import Image  
#p 4128
#q 3096
def pixel(l,p,q):
    for a in range(q):
        for c in range(p):
            mo=0
            for d in range(16):
                for b in range(16):
                    mo=mo+l[a*256*p+b*16*p+c*16+d]
            mo=int(mo/256)
            for d in range(16):
                for b in range(16):
                    l[a*256*p+b*16*p+c*16+d]=mo
    return l
p=9     # 9 carrÃ©s en largeur
q=9     # 9 carrÃ©s en longueur
#ouverture et Ã©clatage de l'image
im = Image.open("ivain.png")
r,g,b=im.split()
#transformation de chaque image en liste 
#et action de la fonction pixel()
r=list(r.getdata())
r=pixel(r,p,q)
g=list(g.getdata())
g=pixel(g,p,q)
b=list(b.getdata())
b=pixel(b,p,q)
#crÃ©ation de trois nouvelles images
nr = Image.new("L",(16*p,16*q))
nr.putdata(r)
ng = Image.new("L",(16*p,16*q))
ng.putdata(g)
nb = Image.new("L",(16*p,16*q))
nb.putdata(b)

#fusion des trois nouvelles images
imgnew = Image.merge('RGB',(nr,ng,nb)) 
imgnew.save("ivainpix.png") 
