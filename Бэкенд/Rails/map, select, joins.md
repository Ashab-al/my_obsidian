@tags = @user.questions.joins(:tags).distinct.pluck(:title)

@tags = @user.questions.select { |question| question.tags.present? }.map(&:tags).first

map(&:tags) - Проитерировать каждый объект и достать tags