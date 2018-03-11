int Grille [ ] [ ] = nouveau int [ 10 ] [ 20 ] ;
Courant Tetromino = nouveau Tetromino ( ) ;
int currentPos [ ] = nouvel int [ 2 ] ;
int timeBuff = 0 ;
score int = 0 ;
 
void setup ( ) {
  taille ( 200 , 375 ) ;
  textFont ( createFont ( "Courier" , 20 ) ) ;
  textAlign ( CENTRE, CENTRE ) ;
  courant = nouveau Tetromino ( ) ;
  currentPos [ 0 ] = 4 ;
  currentPos [ 1 ] = 0 ;
}
 
void keyPressed ( ) {
  if ( keyCode == 37 ) {
    booléen stop = false ;
    pour ( int i = 0 ; i < 4 ; i ++ ) {
      si ( ( en cours. getShapeX ( i ) + CurrentPos [ 0 ] ) > 0 ) {
        si ( ( actuel. getShapeX ( i ) + CurrentPos [ 0 ] ) < 9 && ( courant. getShapeY ( i ) + CurrentPos [ 1 ] ) < 19 && ( actuel. getShapeY ( i ) + CurrentPos [ 1 ] ) > 0 ) {
          if ( Grid [ actuel getShapeX ( i ) + currentPos [ 0 ] - 1 ] [ actuel getShapeY ( i ) + currentPos [ 1 ] ] ! = 0 ) stop = true ;
        }
      } else stop = true ;
    }
    si ( ! stop ) currentPos [ 0 ] -;
  }
  if ( keyCode == 38 ) {
    actuel. pourriture ( ) ;
    if ( current. getMinX ( ) + currentPos [ 0 ] < 0 ) currentPos [ 0 ] - = courant. getMinX ( ) + currentPos [ 0 ] ;
    if ( current. getMaxX ( ) + currentPos [ 0 ] > 9 ) currentPos [ 0 ] - = courant. getMaxX ( ) + currentPos [ 0 ] - 9 ;
    if ( current. getMinY ( ) + currentPos [ 1 ] < 0 ) currentPos [ 1 ] - = courant. getMinY ( ) + currentPos [ 1 ] ;
    if ( current. getMaxY ( ) + currentPos [ 1 ] > 19 ) currentPos [ 1 ] - = courant. getMaxY ( ) + currentPos [ 1 ] - 19 ;
  }
  if ( keyCode == 39 ) {
    booléen stop = false ;
    pour ( int i = 0 ; i < 4 ; i ++ ) {
      si ( ( actuel. getShapeX ( i ) + CurrentPos [ 0 ] ) < 9 ) {
        si ( ( actuel. getShapeX ( i ) + CurrentPos [ 0 ] ) > 0 && ( courant. getShapeY ( i ) + CurrentPos [ 1 ] ) < 19 && ( actuel. getShapeY ( i ) + CurrentPos [ 1 ] ) > 0 ) {
          si ( Grille [ . courant getShapeX ( i ) + CurrentPos [ 0 ] + 1 ] [ . courant getShapeY ( i ) + CurrentPos [ 1 ] ] ! = 0 ) arrêtent = true ;
        }
      } else stop = true ;
    }
    if ( ! stop ) currentPos [ 0 ] ++;
  }
  if ( keyCode == 40 ) {
    score ++;
    currentPos [ 1 ] ++;
    verifyGrid ( ) ;
  }
}
 
void draw ( ) {
  arrière-plan ( 0 ) ;
  noStroke ( ) ;
  pour ( int x = 0 ; x < 10 ; x ++ ) {
    pour ( int y = 0 ; y < 20 ; y ++ ) {
      if ( Grille [ x ] [ y ] == 0 ) remplir ( 100 ) ;
      sinon if ( Grid [ x ] [ y ] == 1 ) fill ( 50 , 150 , 255 ) ;
      sinon if ( Grid [ x ] [ y ] == 2 ) fill ( 0 , 0 , 255 ) ;
      sinon if ( Grid [ x ] [ y ] == 3 ) fill ( 255 , 150 , 0 ) ;
      sinon if ( Grid [ x ] [ y ] == 4 ) fill ( 255 , 255 , 0 ) ;
      sinon if ( Grid [ x ] [ y ] == 5 ) fill ( 100 , 255 , 0 ) ;
      sinon if ( Grid [ x ] [ y ] == 6 ) fill ( 150 , 0 , 150 ) ;
      else fill ( 255 , 0 , 0 ) ;
      rect ( x * 15 + 25 , y * 15 + 25 , 13 , 13 ) ;
    }
  }
 
  displayCurrent ( ) ;
 
  timeBuff ++;
  if ( timeBuff > 20 ) {
    timeBuff = 0 ;
    currentPos [ 1 ] ++;
  }
 
  verifyGrid ( ) ;
 
  texte ( "Score:" + score, 100 , 345 ) ;
}
 
public void verifyGrid ( ) {
  booléen stop = false ;
 
  pour ( int i = 0 ; i < 4 ; i ++ ) {
    if ( current. getShapeY ( i ) + currentPos [ 1 ] < 19 ) {
      if ( Grid [ actuel getShapeX ( i ) + currentPos [ 0 ] ] [ actuel getShapeY ( i ) + currentPos [ 1 ] + 1 ] ! = 0 ) {
        stop = vrai ;
      }
    }
  }
 
  si ( courant. getMaxY ( ) + CurrentPos [ 1 ] == 19 || arrêt ) {
    pour ( int i = 0 ; i < 4 ; i ++ ) {
      si ( ( actuel. getShapeY ( i ) + CurrentPos [ 1 ] ) < 0 ) {
        perdu ( ) ;
      } D'autre grille [ ( courant. GetShapeX ( i ) + CurrentPos [ 0 ] ) ] [ ( actuel. GetShapeY ( i ) + CurrentPos [ 1 ] ) ] = courant. getColor ( ) ;
    }
    nombre entier = 0 ;
    pour ( int y = 0 ; y < 20 ; y ++ ) {
      booléen destroy = true ;
      pour ( int x = 0 ; x < 10 ; x ++ ) {
        if ( Grille [ x ] [ y ] == 0 ) détruit = faux ;
      }
      si ( détruire ) {
        compter ++;
        pour ( int y2 = y - 1 ; y2 > - 1 ; y2 - ) {
          pour ( int x = 0 ; x < 10 ; x ++ ) {
            Grille [ x ] [ y2 + 1 ] = Grille [ x ] [ y2 ] ;
          }
        }
      }
    }
    if ( nombre > 0 ) {
      si ( compte == 1 ) score + = 40 ;
      sinon si ( compte == 2 ) score + = 100 ;
      sinon si ( compte == 3 ) score + = 300 ;
      autre score + = 1200 ;
    }
 
    courant = nouveau Tetromino ( ) ;
    currentPos [ 0 ] = 4 ;
    currentPos [ 1 ] = 0 ;
 
    displayCurrent ( ) ;
 
    pour ( int i = 0 ; i < 4 ; i ++ ) {
      if ( current. getShapeY ( i ) + currentPos [ 1 ] < 19 ) {
        if ( Grid [ actuel getShapeX ( i ) + currentPos [ 0 ] ] [ actuel getShapeY ( i ) + currentPos [ 1 ] + 1 ] ! = 0 ) {
          perdu ( ) ;
        }
      }
    }
  }
}
 
void lost ( ) {
  remplir ( 0 , 200 ) ;
  rect ( 0 , 0 , largeur, hauteur ) ;
  remplir ( 255 ) ;
  texte ( "Score:" + score, 100 , 345 ) ;
  noLoop ( ) ;
}
 
void displayCurrent ( ) {
  si ( . courant getColor ( ) == 0 ) remplir ( 100 ) ;
  d'autre si ( . courant getColor ( ) == 1 ) de remplissage ( 50 , 150 , 255 ) ;
  d'autre si ( . courant getColor ( ) == 2 ) remplir ( 0 , 0 , 255 ) ;
  d'autre si ( . courant getColor ( ) == 3 ) de remplissage ( 255 , 150 , 0 ) ;
  d'autre si ( . courant getColor ( ) == 4 ) de remplissage ( 255 , 255 , 0 ) ;
  d'autre si ( . courant getColor ( ) == 5 ) de remplissage ( 100 , 255 , 0 ) ;
  d'autre si ( . courant getColor ( ) == 6 ) de remplissage ( 150 , 0 , 150 ) ;
  else fill ( 255 , 0 , 0 ) ;
 
  pour ( int i = 0 ; i < 4 ; i ++ ) {
    si ( ( actuel. getShapeY ( i ) + CurrentPos [ 1 ] ) > = 0 ) {
      rect ( ( . courant getShapeX ( i ) + CurrentPos [ 0 ] ) * 15 + 25 , ( courant. getShapeY ( i ) + CurrentPos [ 1 ] ) * 15 + 25 , 13 , 13 ) ;
    }
  }
}
 
classe Tetromino {
  forme int [ ] [ ] = nouveau int [ 4 ] [ 2 ] ;
  int col = 0 ;
  Tetromino public ( ) {
    col = int ( aléatoire ( 1 , 8 ) ) ;
    if ( col == 1 ) {
      forme [ 1 ] [ 0 ] = 1 ;
      forme [ 2 ] [ 0 ] = - 1 ;
      forme [ 3 ] [ 0 ] = - 2 ;
    } else if ( col == 2 ) {
      forme [ 1 ] [ 0 ] = 1 ;
      forme [ 2 ] [ 0 ] = - 1 ;
      forme [ 3 ] [ 0 ] = - 1 ;
      forme [ 3 ] [ 1 ] = - 1 ;
    } else if ( col == 3 ) {
      forme [ 1 ] [ 0 ] = 1 ;
      forme [ 2 ] [ 0 ] = - 1 ;
      forme [ 3 ] [ 0 ] = 1 ;
      forme [ 3 ] [ 1 ] = - 1 ;
    } else if ( col == 4 ) {
      forme [ 1 ] [ 0 ] = 1 ;
      forme [ 2 ] [ 1 ] = 1 ;
      forme [ 3 ] [ 0 ] = 1 ;
      forme [ 3 ] [ 1 ] = 1 ;
    } else if ( col == 5 ) {
      forme [ 1 ] [ 0 ] = - 1 ;
      forme [ 2 ] [ 1 ] = - 1 ;
      forme [ 3 ] [ 0 ] = 1 ;
      forme [ 3 ] [ 1 ] = - 1 ;
    } else if ( col == 6 ) {
      forme [ 1 ] [ 0 ] = 1 ;
      forme [ 2 ] [ 0 ] = - 1 ;
      forme [ 3 ] [ 1 ] = - 1 ;
    } else {
      forme [ 1 ] [ 0 ] = 1 ;
      forme [ 2 ] [ 1 ] = - 1 ;
      forme [ 3 ] [ 0 ] = - 1 ;
      forme [ 3 ] [ 1 ] = - 1 ;
    }
  }
  public int getShapeX ( int i ) {
    forme de retour [ i ] [ 0 ] ;
  }
  public int getShapeY ( int i ) {
    forme de retour [ i ] [ 1 ] ;
  }
  public int getMaxX ( ) {
    int i = 0 ;
    pour ( int j = 0 ; j < 4 ; j ++ ) {
      if ( forme [ j ] [ 0 ] > forme [ i ] [ 0 ] ) i = j ;
    }
    forme de retour [ i ] [ 0 ] ;
  }
  public int getMaxY ( ) {
    int i = 0 ;
    pour ( int j = 0 ; j < 4 ; j ++ ) {
      if ( forme [ j ] [ 1 ] > forme [ i ] [ 1 ] ) i = j ;
    }
    forme de retour [ i ] [ 1 ] ;
  }
  public int getMinX ( ) {
    int i = 0 ;
    pour ( int j = 0 ; j < 4 ; j ++ ) {
      if ( forme [ j ] [ 0 ] < forme [ i ] [ 0 ] ) i = j ;
    }
    forme de retour [ i ] [ 0 ] ;
  }
  public int getMinY ( ) {
    int i = 0 ;
    pour ( int j = 0 ; j < 4 ; j ++ ) {
      if ( forme [ j ] [ 1 ] < forme [ i ] [ 1 ] ) i = j ;
    }
    forme de retour [ i ] [ 1 ] ;
  }
  public int getColor ( ) {
    retour col ;
  }
  public void rot ( ) {
    pour ( int i = 0 ; i < 4 ; i ++ ) {
      int buf = forme [ i ] [ 0 ] ;
      forme [ i ] [ 0 ] = forme [ i ] [ 1 ] ;
      forme [ i ] [ 1 ] = - buf ;
    }
  }
}
